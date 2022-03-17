---
title: "Base de données des topologies"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 4
---

La base de données est la mémoire de notre projet. C'est l'outil qui va nous permettre de stocker l'intégralité des différentes topologies, mais, également de les retrouver quand nécessaire. Les fichiers de topologie peuvent ressembler à ceci :

```config
  {
    "name": "Vlan1",
    "description": "Vlan1",
    "port_id": 1,
    "status": "up",
    "operstatus": "up",
    "vlan": null,
    "speed": 1000000000
  },
  {
    "name": "Vlan10",
    "description": "Vlan10",
    "port_id": 10,
    "status": "up",
    "operstatus": "up",
    "vlan": null,
    "speed": 1000000000
  },
  {
    "name": "StackPort1",
    "description": "StackPort1",
    "port_id": 5179,
    "status": "up",
    "operstatus": "up",
    "vlan": null,
    "speed": 0
  },
  ```

C'est donc ainsi que les informations nécessaires à la configuration seront stockées dans notre base de données.

Mais ces informations peuvent venir sous trois formes :

La première est dans le cas de la configuration d'un vlan. Dans ce cas, chez cisco il est nécessaire de faire :

```config
SWITCH(config)#vlan {numero}
SWITCH(config-vlan)#name {name}
```

Ce qui dans notre base de données ce résumera par :

```json
  {
    "description": "{name}",
    "dot1q_id": {numero}
  },
```

Le second cas est celui d'une interface en mode **trunk**, ce qui nécessite de faire :

```config
SWITCH(config)#interface fastethernet 0/1
SWITCH(config-if)#switchport mode trunk
```

Dans notre cas, on obtiendra :

```json
  {
    "interface": {
      "name": "FastEthernet2/0/47",
      "description": "FastEthernet2/0/47",
      "port_id": 10547,
      "status": "up",
      "operstatus": "down",
      "vlan": null,
      "speed": 100000000
    },
    "native_vlan": {
      "description": "RT2G1B6-0",
      "dot1q_id": 415
    },
    "tagged_vlans": [
      0,
      4,
      8,
      16,
      26,
      351,
      352,
      353
    ],
```

Le dernier cas que nous pouvons rencontrer est le cas d'une interface en mode **access** qui-ce traduit en cisco par :

```config
SWITCH(config)#interface ethernet0/1
SWITCH(config-if)#switchport mode access
```

Ce qui deviendra dans la base de données :

```json
  {
    "name": "FastEthernet1/0/38",
    "description": "FastEthernet1/0/38",
    "port_id": 10038,
    "status": "up",
    "operstatus": "down",
    "vlan": {
      "description": "rt-reseau-1",
      "dot1q_id": 64
    },
```

Toutes les configurations que nous enregistrons dans la base de données, ne sont pas à faire manuellement, il est possible de récupérer une configuration qui est déjà en production ou encore dans créer une nouvelle au travers de l'interface web, ce qui rend la création bien plus simple.