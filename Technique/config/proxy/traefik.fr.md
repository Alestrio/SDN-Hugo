---
title: "Traefik Reverse Proxy"
date: 2021-12-21T10:35:34+02:00
draft: false
tags: ["useful","config","proxy","production"]
weight: 5
---

Nous avons vu dans les chapitres précédents, la configuration du reverse-proxy NGINX. Cependant, aujourd'hui, avec Docker, NGINX est un peu obsolète, et il existe des solutions plus dynamiques comme Traefik, dont nous allons parler dans cet article.

## Le reverse proxy Traefik

Traefik est un __reverse-proxy__ (aussi appelé _edge router_) open-source. \
Un reverse proxy est un programme qui gère l'accès à des serveurs dans un réseau qui se trouve derrière lui, en ajoutant de la sécurité, de la journalisation, et parfois, du chiffrement.

La particularité de Traefik est sa fonction de __découverte de services__, ce qui signifie qu'il travaille avec Docker afin de créer sa configuration pour les conteneurs qui sont en cours. \
Il faut pour cela, lui donner le chemin du socket Docker, ce que l'on verra dans la partie suivante, la <ins>configuration</ins>

## Configuration

La configuration du reverse-proxy __Traefik__ est très simple. Tout d'abord, il faut __instancier__ un container Traefik dans le fichier __docker-compose__ :

```yaml
  reverse-proxy:
    # The official v2.0 Traefik docker image
    image: traefik:latest
    # Enables the web UI and tells Traefik to listen to docker
    command:
      --api.insecure=true
      --providers.docker
      --entrypoints.web.address=:80
    ports:
      # The HTTP port
      - "80:80"
      # The Web UI (enabled by --api.insecure=true)
      - "8080:8080"
    volumes:
      # So that Traefik can listen to the Docker events
      - /var/run/docker.sock:/var/run/docker.sock
      - /home/user/compose/traefik/traefik.toml:/etc/traefik/traefik.toml
      - /home/user/compose/traefik/acme.json:/acme.json
      - /home/user/compose/traefik/access.log:/var/log/access.log
    networks:
        backend:
```

Ensuite, on édite le fichier de configuration :

```toml
[api]
  dashboard = true # Active le panneau de contrôle..
  insecure = true #.. en http

[entryPoints]
  [entryPoints.web]
    address = ":80" # Définis le port 80 comme entrée

[providers]
  [providers.docker]
    watch = true
    exposedByDefault = false
    network = "backend" # Active la découverte de services dockers, sur le réseau "backend"

[accessLog]
  filePath = "/var/log/access.log" # Fichier de logs

[pilot]
    token = "un-token" # Token pour le service web "pilot"
```

On peut ensuite activer le service sur les différents containers :

```yaml
  hugo:
    image: nginx:latest
    restart: always
    volumes:
      - /home/user/compose/hugo/sdn_notice/public/:/usr/share/nginx/html/
    labels:
        - "traefik.enable=true" # Active le reverse-proxy pour ce container
        - "traefik.http.routers.doc.rule=Host(`doc.sdn.chalons.univ-reims.fr`)" # Permet de définir l'URL d'accès
    networks:
        backend:
    [...]
  api_r1:
    [...]
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.api_r1.loadbalancer.server.port=8000" # Permet de spécifier le port cible
      - "traefik.http.routers.api_r1.rule=Host(`r1.api.sdn.chalons.univ-reims.fr`)"
```

## L'interface web

Une fois la configuration effectuée, on peut accéder à l'interface web, qui tourne sur le port 8080 :

![dashboard1](../../../../images/dashboard1.png)

![dashboard21](../../../../images/dashboard2.png)

Cette interface est uniquement informative, aucune configuration ne peut être faite à partir d'elle.