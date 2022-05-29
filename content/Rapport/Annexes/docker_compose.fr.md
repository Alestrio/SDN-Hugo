---
title: "6. Fichier Docker-compose"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

```yaml

version: "3"


services:
  hugo:
    image: nginx:latest
    restart: always
    volumes: 
      - /home/user/compose/hugo/sdn_notice/public/:/usr/share/nginx/html/
    labels:
        - "traefik.enable=true"
        - "traefik.http.routers.doc.rule=Host(`doc.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  reverse-proxy:
    # The official v2.0 Traefik docker image
    image: traefik:latest
    # Enables the web UI and tells Traefik to listen to docker
    restart: always
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
  api_r1:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
    volumes:
      - /home/user/compose/api/r1/config.yaml:/home/api/config/config.yaml:ro
    environment:
      - CONFIG_DIR=/home/api/config/
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.api_r1.loadbalancer.server.port=8000" 
      - "traefik.http.routers.api_r1.rule=Host(`r1.api.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  api_r2:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
    volumes:
      - /home/user/compose/api/r2/config.yaml:/home/api/config/config.yaml:ro
    environment:
      - CONFIG_DIR=/home/api/config/
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.api_r2.loadbalancer.server.port=8000"
      - "traefik.http.routers.api_r2.rule=Host(`r2.api.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  api_r3:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
    volumes:
      - /home/user/compose/api/r3/config.yaml:/home/api/config/config.yaml:ro
    environment:
      - CONFIG_DIR=/home/api/config/
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.api_r3.loadbalancer.server.port=8000"
      - "traefik.http.routers.api_r3.rule=Host(`r3.api.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  api_test:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
    volumes:
      - /home/user/compose/api/test/config.yaml:/home/api/config/config.yaml:ro
    environment:
      - CONFIG_DIR=/home/api/config/
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.api_test.loadbalancer.server.port=8000" 
      - "traefik.http.routers.api_test.rule=Host(`test.api.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  app:
    restart: always
    image: europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-app:latest
    labels:
      - "traefik.enable=true"
      - "traefik.http.services.app.loadbalancer.server.port=5000"
      - "traefik.http.routers.app.rule=Host(`www.sdn.chalons.univ-reims.fr`)"
    networks:
        backend:
  bind:
    restart: always
    image: sameersbn/bind:latest
    ports:
      - "53:53/udp"
      - "53:53/tcp"
      - "10000:10000/tcp"
    volumes:
      - /home/user/compose/bind/:/data
networks:
  backend:
```