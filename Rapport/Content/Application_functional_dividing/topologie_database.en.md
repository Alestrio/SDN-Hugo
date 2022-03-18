---
title: "Topologie database"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 4
---

The database is the memory of our project. It is the tool that will allow us to store all the different topologies, but also to retrieve them when necessary. The topology files can look like this:

```json
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
  }
  ```
  
(see Appendix 5)

This is how the information needed for the configuration will be stored in our database.

But this information can come in three forms:

The first is in the case of the configuration of a vlan. In this case, in cisco it is necessary to do :

```config
SWITCH(config)#vlan {numero}
SWITCH(config-vlan)#name {name}
```

Which in our database will be summarized as:

```json
  {
    "description": "{name}",
    "dot1q_id": {numero}
  }
```

The second case is that of an interface in **trunk** mode, which requires to do :

```config
SWITCH(config)#interface fastethernet 0/1
SWITCH(config-if)#switchport mode trunk
```

In our case, we will get :

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

The last case we may encounter is the case of an interface in **access** mode which translates in Cisco dialect as :

```config
SWITCH(config)#interface ethernet0/1
SWITCH(config-if)#switchport mode access
```

This will result in the database:

```json
  {
    "name": "FastEthernet1/0/38",
    "description": "FastEthernet1/0/38",
    "port_id": 10038,
    "status": "up",
    "operstatus": "down",
    "vlan": {
      "description": "rt-network-1",
      "dot1q_id": 64
    },
```

All the configurations that we save in the database, do not have to be done manually, it is possible to retrieve a configuration that is already in production or to create a new one through the web interface, which makes the creation much easier.
