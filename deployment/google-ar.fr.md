---
title: "Google Artifact Registry"
date: 2021-12-21T18:17:10Z
tags: ["notice", "docker", "compose", "Google"]
draft: false
---

Originellement, l'hébergement de l'image Docker se faisait sur DockerHub, qui propose l'hébergement d'___UNE___ image Docker privée. Notre projet en nécessite au minimum deux, ainsi, il a fallu trouver d'autres solutions.

## Google Cloud Platform

Et c'est dans nos recherches que nous avons découvert __Google Cloud Platform__, aussi appelé "__GCP__". \
Cet ensemble d'outils cloud signé Google propose un service d'hébergement de conteneurs Docker appelé __Google Artifact Registry__, et propose une offre d'essai comprenant 300$ pendant 90j. \
Vu l'aspect bon marché de cette solution (prix ici : https://cloud.google.com/artifact-registry/pricing) et le crédit qui nous est offert, nous avons décidé de profiter de cette offre, afin de mettre à niveau notre hébergement d'images Docker.

## Collaboration

L'autre avantage de cette plateforme est que l'on peut désigner des personnes qui pourront gérer le registre en plus de la personne qui a l'abonnement. \
Cela permet une plus grande __autonomie__ des membres de l'équipe, et permet l'utilisation d'autres services (VMWare, Cloud Build) par d'autres personnes sur le même abonnement.

## Configuration

Evidemment, un changement de plateforme veut aussi dire un changement de configuration ! Voici les choses qui ont changé :

- Tout d'abord, il a fallu mettre en place les outils Google sur la machine de production (documentation ici : https://cloud.google.com/sdk/docs/install)

- Ensuite, il a fallu initialiser l'authentification sur les services Google (documentation ici : https://cloud.google.com/artifact-registry/docs/docker/quickstart)

- Ensuite, changement de la CI/CD :
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

- Enfin, changement du docker-compose.yaml :

```yaml
api_r1:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
```