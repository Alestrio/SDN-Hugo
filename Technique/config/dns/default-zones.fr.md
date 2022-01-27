---
title: "Default-Zones"
date: 2021-10-21T17:18:05+02:00
draft: false
weight: 5
tags: ["useful","config","dns","alpine1"]
---

### named.conf.default-zones

```
// prime the server with knowledge of the root servers
zone "." {
    type hint;
    file "/usr/share/dns/root.hints";
};

// be authoritative for the localhost forward and reverse zones, and for
// broadcast zones as per RFC 1912

zone "localhost" {
    type master;
    file "/etc/bind/db.local";
};

zone "127.in-addr.arpa" {
    type master;
    file "/etc/bind/db.127";
};

zone "0.in-addr.arpa" {
    type master;
    file "/etc/bind/db.0";
};

zone "255.in-addr.arpa" {
    type master;
    file "/etc/bind/db.255";
};


zone "cloudstack.chalons.univ-reims.fr" {
    type master;
    file "/etc/bind/zone.cloudstack.chalons.univ-reims.fr";
};

zone "sdn.chalons.univ-reims.fr" {
    type master;
    file "/etc/bind/zone.sdn.chalons.univ-reims.fr";
};

zone "chalons.univ-reims.fr"{
    type forward;
    forwarders {10.59.50.20;10.59.50.10;};
};

```
