---
title: "Config Proxy pour Hugo"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["useful","config","proxy","alpine1"]
weight: 5
---
### hugo.conf (Pour le site ou vous êtes en ce moment)

```
map $sent_http_content_type $expires {
    "text/html"                 epoch;
    "text/html; charset=utf-8"  epoch;
    default                     off;
}

server {
    listen          80;             # the port nginx is listening on
    server_name     doc.sdn.chalons.univ-reims.fr;
    gzip            on;
    gzip_types      text/plain application/xml text/css application/javascript;
    gzip_min_length 1000;
    location / {
        expires $expires;
        proxy_redirect                      off;
        proxy_set_header Host               $host;
        proxy_set_header X-Real-IP          $remote_addr;
        proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto  $scheme;
        proxy_read_timeout          1m;
        proxy_connect_timeout       1m;
        proxy_pass                          http://hugo; # set the address of the Node.js instance here
    }
}

```
