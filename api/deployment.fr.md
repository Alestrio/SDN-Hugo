---
title: "Déploiement de l'API"
date: 2021-10-17T12:42:10Z
tags: ["notice", "docker", "compose", "fastapi"]
draft: false
---

## Prérequis

Nous avons vu dans la partie _config_ que le déploiement de notre __API__ sur DockerHub est automatisé grâce à une __GithubRunner__. \
Nous allons donc nous servir de l'image docker générée afin de déclarer de nouvelles instances de notre API.

## Docker-Compose

Voici un exemple de configuration d'instanciation de l'API sur Docker-Compose :

```yaml
  api_r1:
    image: alestrio/sdn-cloudstack  # Nom de l'image de base
    ports:
      - "8064:8000"  # Exposition de port (bientôt obsolète, voir partie proxy.....)
    volumes:
      - /home/user/compose/api/r1/config.yaml:/home/api/config/config.yaml:ro  # Fichier de configuration
    environment:
      - CONFIG_DIR=/home/api/config/  # Déclaration position fichier de configuration
```

## Proxy

...

## Configuration automatisée

...