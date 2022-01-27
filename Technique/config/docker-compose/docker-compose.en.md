---
title: "Docker-Compose"
date: 2021-10-21T17:11:26+02:00
tags: ["useful","config","docker","alpine1"]
draft: false
---

## docker-compose.yml

```yml
version: "3"


services:
  hugo:
    image: nginx:latest
    volumes: 
      - /home/user/compose/hugo/sdn_notice/public/:/usr/share/nginx/html/
    networks:
        backend:
  proxy:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /home/user/compose/proxy:/etc/nginx/conf.d/:ro
    networks:
        backend:
  application:
    image: nginx:latest
    volumes:
      - /home/user/compose/application/:/usr/share/nginx/html/
    networks:
        backend:
  proxy:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /home/user/compose/proxy:/etc/nginx/conf.d/:ro
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
  mongo:
    image: mongo
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: iutchalons
    ports:
      - "27017:27017"
    networks:
        backend:
networks:
  backend:

```
