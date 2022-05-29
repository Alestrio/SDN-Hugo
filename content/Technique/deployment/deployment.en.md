---
title: "API Deployment"
date: 2021-10-17T12:42:10Z
tags: ["notice", "docker", "compose", "fastapi"]
draft: false
---

## Prerequisites

We have seen in the _config_ part that the deployment of our __API__ on DockerHub is automated thanks to a __GithubRunner__. \
So we will use the generated docker image to declare new instances of our API.

## Docker-Compose

Here is an example of the API instantiation configuration on Docker-Compose:

```yaml
  api_r1:
    image: alestrio/sdn-cloudstack # Base image name
    ports:
      - "8064:8000" # Port exposure (soon deprecated, see proxy..... part)
    volumes:
      - /home/user/compose/api/r1/config.yaml:/home/api/config/config.yaml:ro # Configuration file
    environment:
      - CONFIG_DIR=/home/api/config/ # Declaration position configuration file
```

## Proxy

...

## Automated configuration

...