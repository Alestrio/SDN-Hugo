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