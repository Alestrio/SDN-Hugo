---
title: "7. CICD File"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

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
    - name: Build the Docker image for api
      run: docker image build . --file Dockerfile --tag europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Build the Docker image for app
      run: docker image build . --file Dockerfile --tag europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-app:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack/src/app
    - name: Docker push
      run: docker image push europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-cloudstack:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack
    - name: Docker push
      run: docker image push europe-west1-docker.pkg.dev/sdn-cloudstack/alestrio/sdn-app:latest
      working-directory: /home/user/SDN-Cloudstack/SDN-Cloudstack/src/app
    - name: Docker stop
      run: docker-compose down
      working-directory: /home/user/compose/compose
    - name: Docker reup
      run: docker-compose up -d
      working-directory: /home/user/compose/compose
```