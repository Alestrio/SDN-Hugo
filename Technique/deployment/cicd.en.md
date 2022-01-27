---
title: "CI/CD : Continuous Integration / Continuous Developpement"
date: 2021-10-17T12:42:10Z
tags: ["notice", "cicd", "github", "deploiement"]
draft: false
---

This article is about the CI/CD we are applying for our project.

## Documentation

We use __Github__ to store the sources of the documentation (this website). So, to deploy new versions, we decided to use a __CI/CD__. CI/CD stands for Continuous Integration / Continuous Development, and allows to automate the testing and the deployment part of a project.

First of all, we have to configure the hosting machine. Since our site is self-hosted, we are going to use what is called a "__self-hosted github runner__", whose documentation can be found here: https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners 

Thus, the Github platform automatically generates the scripts and commands we need, in order to install our runner.

Then, we configure the "github actions" part. \
A Github action is a YAML file in the folder : __.github/workflows__ and describes a sequence of instructions to execute when updating a branch.

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: hugo_sdn_hugo
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

      - name: Pull new version
        run: git pull
        working-directory: /home/user/compose/hugo/sdn_notice/content

      - name: Deploy
        run: hugo
        working-directory: /home/user/compose/hugo/sdn_notice/
```

This script allows you to automate the update of the documentation on the server during a "push" on the "main" branch.

## API

We also use Github to store the sources of our __API__, so we naturally chose to create a __CI/CD__ also for this part of our project. \
The purpose of this CI/CD is to automate the creation of a __Docker__ container from our API.

Here is the file related to these actions:

```yaml
name: Docker Image CI # Action name

on:
  push:
    branches: [ main ] # When pushing on the MAIN branch
  pull_request:
    branches: [ main ] # When PRing the MAIN branch

jobs:
  build:
    runs-on: sdn-api # Runs on the runner installed on the datacenter machine
    steps:
    - uses: actions/checkout@v2 # Retrieves the latest version of the project
      with:
        fetch-depth: 0
    - name: Docker login 
     # Connect to DockerHub with the login/password contained on the Github platform in "secrets
      env:
        DOCKER_USER: ${{secrets.DOCKER_USER}}
        DOCKER_PASSWORD: ${{secrets.DOCKER_PASSWORD}}
      run: |
        docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Build the Docker image  
    # Build the docker image from the Dockerfile
      run: docker image build . --file Dockerfile --tag alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Docker push 
     # Send the Docker image online to DockerHub
      run: docker image push ${{secrets.DOCKER_USER}}/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
```

So, at each __push__ on the __main__ branch (the production branch), __the Docker__ image of the project is regenerated and sent to __DockerHub__, then we just have to restart the Docker-Compose at the end, an automatable task, but we want to keep it manual, since it is a production machine.