---
title: "Exemple de topologie"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

```json
{
  "name": null,
  "hostname": "\"RT-RES1.chalons.univ-reims.fr\"",
  "interfaces": [
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
    {
      "name": "StackSub-St1-1",
      "description": "StackSub-St1-1",
      "port_id": 5180,
      "status": "up",
      "operstatus": "up",
      "vlan": null,
      "speed": 0
    },
    {
      "name": "StackSub-St1-2",
      "description": "StackSub-St1-2",
      "port_id": 5181,
      "status": "up",
      "operstatus": "up",
      "vlan": null,
      "speed": 0
    },
    {
      "name": "StackPort2",
      "description": "StackPort2",
      "port_id": 5182,
      "status": "up",
      "operstatus": "up",
      "vlan": null,
      "speed": 0
    },
    {
      "name": "StackSub-St2-1",
      "description": "StackSub-St2-1",
      "port_id": 5183,
      "status": "up",
      "operstatus": "up",
      "vlan": null,
      "speed": 0
    },
    {
      "name": "StackSub-St2-2",
      "description": "StackSub-St2-2",
      "port_id": 5184,
      "status": "up",
      "operstatus": "up",
      "vlan": null,
      "speed": 0
    },
    {
      "name": "FastEthernet1/0/1",
      "description": "FastEthernet1/0/1",
      "port_id": 10001,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-1",
        "dot1q_id": 201
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/2",
      "description": "FastEthernet1/0/2",
      "port_id": 10002,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-2",
        "dot1q_id": 202
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/3",
      "description": "FastEthernet1/0/3",
      "port_id": 10003,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-3",
        "dot1q_id": 203
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/4",
      "description": "FastEthernet1/0/4",
      "port_id": 10004,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-4",
        "dot1q_id": 204
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/5",
      "description": "FastEthernet1/0/5",
      "port_id": 10005,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-5",
        "dot1q_id": 205
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/6",
      "description": "FastEthernet1/0/6",
      "port_id": 10006,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-6",
        "dot1q_id": 206
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/7",
      "description": "FastEthernet1/0/7",
      "port_id": 10007,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-7",
        "dot1q_id": 207
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/8",
      "description": "FastEthernet1/0/8",
      "port_id": 10008,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-8",
        "dot1q_id": 208
      },
      "speed": 10000000
    },
    {
      "name": "FastEthernet1/0/9",
      "description": "FastEthernet1/0/9",
      "port_id": 10009,
      "status": "up",
      "operstatus": "down",
      "vlan": {
        "description": "SALLE-RT1-PORT-9",
        "dot1q_id": 209
      },
      "speed": 10000000
    },
   [...]
  ],
  "vlans": [
    {
      "description": "rt-reseau-2",
      "dot1q_id": 68
    },
    {
      "description": "rt-reseau-3",
      "dot1q_id": 72
    },
    {
      "description": "RT1G1B1-0",
      "dot1q_id": 300
    },
    {
      "description": "RT1G1B1-1",
      "dot1q_id": 301
    },
    {
      "description": "RT1G1B1-2",
      "dot1q_id": 302
    },
    {
      "description": "RT1G1B2-0",
      "dot1q_id": 303
    },
    {
      "description": "RT1G1B2-1",
      "dot1q_id": 304
    },
    {
      "description": "RT1G1B2-2",
      "dot1q_id": 305
    },
    {
      "description": "RT1G1B3-0",
      "dot1q_id": 306
    },
   [...]
  ],
  "trunks": [
    {
      "interface": {
        "name": "FastEthernet2/0/32",
        "description": "FastEthernet2/0/32",
        "port_id": 10532,
        "status": "up",
        "operstatus": "down",
        "vlan": null,
        "speed": 100000000
      },
      "native_vlan": {
        "description": "RT2G1B1-0",
        "dot1q_id": 400
      },
      "tagged_vlans": [
        0,
        4,
        8,
        16,
        26,
        336,
        337,
        338
      ],
      "status": "1"
    },
    {
      "interface": {
        "name": "FastEthernet2/0/33",
        "description": "FastEthernet2/0/33",
        "port_id": 10533,
        "status": "up",
        "operstatus": "down",
        "vlan": null,
        "speed": 100000000
      },
      "native_vlan": {
        "description": "RT2G1B2-0",
        "dot1q_id": 403
      },
      "tagged_vlans": [
        0,
        4,
        8,
        16,
        26,
        339,
        340,
        341
      ],
      "status": "1"
    },
    {
      "interface": {
        "name": "FastEthernet2/0/34",
        "description": "FastEthernet2/0/34",
        "port_id": 10534,
        "status": "up",
        "operstatus": "down",
        "vlan": null,
        "speed": 100000000
      },
      "native_vlan": {
        "description": "RT2G1B3-0",
        "dot1q_id": 406
      },
      "tagged_vlans": [
        0,
        4,
        8,
        16,
        26,
        342,
        343,
        344
      ],
      "status": "1"
    },
    {
      "interface": {
        "name": "FastEthernet2/0/35",
        "description": "FastEthernet2/0/35",
        "port_id": 10535,
        "status": "up",
        "operstatus": "down",
        "vlan": null,
        "speed": 100000000
      },
      "native_vlan": {
        "description": "RT2G1B4-0",
        "dot1q_id": 409
      },
      "tagged_vlans": [
        0,
        4,
        8,
        16,
        26,
        345,
        346,
        347
      ],
      "status": "1"
    },
    [...]
  ]
}
```