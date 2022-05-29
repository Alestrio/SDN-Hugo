---
title: "Google Artifact Registry"
date: 2021-12-21T18:17:10Z
tags: ["notice", "docker", "compose", "google"]
draft: false
---

Originally, the Docker image hosting was done on DockerHub, which offers hosting of ___ONE___ private Docker image. Our project requires at least two, so we had to find other solutions.

## Google Cloud Platform

And it is in our research that we discovered __Google Cloud Platform__, also called "__GCP__". \
This set of cloud tools signed by Google offers a Docker container hosting service called __Google Artifact Registry__, and offers a trial offer including $300 for 90 days. \
Considering the cheapness of this solution (price here: https://cloud.google.com/artifact-registry/pricing) and the credit offered to us, we decided to take advantage of this offer, in order to upgrade our Docker image hosting.

## Collaboration

The other advantage of this platform is that you can designate people to manage the registry in addition to the person who has the subscription. \
This allows greater __autonomy__ of the team members, and allows the use of other services (VMWare, Cloud Build) by other people on the same subscription.

## Configuration

Obviously, a change of platform also means a change of configuration! Here are the things that have changed:

- First, we had to set up Google tools on the production machine (documentation here: https://cloud.google.com/sdk/docs/install)

- Then, we had to initialize the authentication on the Google services (documentation here: https://cloud.google.com/artifact-registry/docs/docker/quickstart)

- Then, change the CI/CD:
```yaml
name: Docker Image CI

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: sdn-api
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
    - name: Docker login
      env:
        DOCKER_USER: ${{secrets.DOCKER_USER}}
        DOCKER_PASSWORD: ${{secrets.DOCKER_PASSWORD}}
      run: |
        docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Build the Docker image
      run: docker image build . --file Dockerfile --tag europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Docker push
      run: docker image push europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
```

- Finally, change the docker-compose.yaml :

```yaml
api_r1:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
```