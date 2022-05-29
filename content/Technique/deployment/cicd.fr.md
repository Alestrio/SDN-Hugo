---
title: "CI/CD : Continuous Integration / Continuous Developpement"
date: 2021-10-17T12:42:10Z
tags: ["notice", "cicd", "github", "deploiement"]
draft: false
---

Cet article traite de la CI/CD que nous appliquons pour notre projet.

## Documentation

Nous utilisons __Github__ afin de stocker les sources de la documentation (ce site web). Ainsi, pour déployer les nouvelles versions, nous avons décidé d'utiliser une __CI/CD__. CI/CD veut dire Continuous Integration / Continuous Developpement, et permet d'automatiser la partie tests et la partie déploiement d'un projet.

Avant toute chose, il faut configurer la machine d'hébergement. Puisque notre site est auto-hébergé, nous allons utiliser ce que l'on appelle un "__self-hosted github runner__", dont la documentation est trouvable ici : https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners 

Ainsi, la plateforme Github génère automatiquement les scripts et commandes dont nous avons besoin, afin d'installer notre runner.

Ensuite, nous configurons la partie "github actions". \
Une action Github est un fichier YAML dans le dossier : __.github/workflows__ et décrit une suite d'instructions à exécuter lors de la mise à jour d'une branche.

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: hugo_sdn_hugo
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Pull new version
        run: git pull
        working-directory: /home/user/compose/hugo/sdn_notice/content

      - name: Deploy
        run: hugo
        working-directory: /home/user/compose/hugo/sdn_notice/
```

Ce script permet d'automatiser la mise à jour de la documentation sur le serveur lors d'un "push" sur la branche "main".

## API

Nous utilisons aussi Github afin de stocker les sources de notre __API__, nous avons donc naturellement choisi de créer une __CI/CD__ aussi pour cette partie de notre projet. \
Le but de cette CI/CD est d'automatiser la création d'un container __Docker__ à partir de notre API.

Voici le fichier lié à ces actions :

```yaml
name: Docker Image CI  # Nom de l'action

on:
  push:
    branches: [ main ]  # Lors d'un push sur la branche MAIN
  pull_request:
    branches: [ main ]  # Lors d'un PR sur la branche MAIN

jobs:
  build:
    runs-on: sdn-api  # Tourne sur le runner installé sur la machine du datacenter
    steps:
    - uses: actions/checkout@v2  # Récupère la dernière version du projet
      with:
        fetch-depth: 0
    - name: Docker login 
     # Se connecte à DockerHub avec les login/password contenus sur la plateforme Github en "secrets"
      env:
        DOCKER_USER: ${{secrets.DOCKER_USER}}
        DOCKER_PASSWORD: ${{secrets.DOCKER_PASSWORD}}
      run: |
        docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Build the Docker image  
    # Crée l'image docker à partir du Dockerfile
      run: docker image build . --file Dockerfile --tag alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Docker push 
     # Envoie l'image Docker en ligne sur DockerHub
      run: docker image push ${{secrets.DOCKER_USER}}/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
```

Ainsi, à chaque __push__ sur la branche __main__ (la branche de production), __l'image Docker__ du projet est regénérée et envoyée sur __DockerHub__, il suffit ensuite pour nous de redémarrer le Docker-Compose à la fin, tâche automatisable, mais que nous voulons garder manuelle, puisque qu'il s'agit d'une machine de production.