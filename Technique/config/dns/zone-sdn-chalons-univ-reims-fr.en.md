---
title: "Zone sdn.chalons.univ-reims.fr"
date: 2021-10-21T17:23:19+02:00
draft: false
weight: 6
tags: ["useful","config","dns","alpine1"]
---

### zone.sdn.chalons.univ-reims.fr

```
;
; BIND zone file for sdn.chalons.univ-reims.fr
;

@	IN	SOA	ns1.sdn.chalons.univ-reims.fr admin.sdn.chalons.univ-reims.fr (
                         20210923         ; Serial
                         120         ; Refresh 2mn
                         60          ; Retry 1mn
                         600         ; Expire 10mn
                         3600 )      ; Negative Cache TTL 1h

; DNS SERVER

sdn.chalons.univ-reims.fr.	IN	NS	ns1.sdn.chalons.univ-reims.fr.

; IP DNS

ns1	IN	A	10.59.50.233

; IP WEB-SERVICE

doc	IN	A	10.59.50.233 ; HUGO
www	IN	A	10.59.50.233 ; APPLICATION/SITE-WEB
 
```
