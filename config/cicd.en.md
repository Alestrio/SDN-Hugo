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