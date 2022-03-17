---
title: "Liste des OIDs"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

```yaml
oids:
  systemName: 1.3.6.1.2.1.1.5
  uptime: 1.3.6.1.2.1.1.3
  cdp_neighbors:
    ip: 1.3.6.1.4.1.9.9.23.1.2.1.1.4
    fqdn: 1.3.6.1.4.1.9.9.23.1.2.1.1.6
    interface: 1.3.6.1.4.1.9.9.23.1.2.1.1.7
    model: 1.3.6.1.4.1.9.9.23.1.2.1.1.8
  interfaces:
    table: 1.3.6.1.2.1.2.2
    oids:
      description: 1.3.6.1.2.1.2.2.1.2
      index: 1.3.6.1.2.1.2.2.1.1
      status: 1.3.6.1.2.1.2.2.1.7
      speed: 1.3.6.1.2.1.2.2.1.5
      vlan: 1.3.6.1.4.1.9.9.68.1.2.2.1.2
      operstatus: 1.3.6.1.2.1.2.2.1.8
      mac_address: 1.3.6.1.2.1.2.2.1.6
      sets:
        vlan: 1.3.6.1.4.1.9.9.68.1.2.2.1.2
        trunk_mode: 1.3.6.1.4.1.9.9.46.1.6.1.1.13
        access: 1.3.6.1.4.1.9.9.46.1.6.1.1.29 # 1-trunk,2-access,3-disabled
    mib_names:
      description: ifDescr
      index: ifIndex
      status: ifAdminStatus
      speed: ifSpeed
      operstatus: ifOperStatus
      mac_address: ifPhysAddress
  trunks:
    table: 1.3.6.1.4.1.9.9.46.1.6.1
    oids:
      index: 1.3.6.1.4.1.9.9.46.1.6.1.1.1
      domain: 1.3.6.1.4.1.9.9.46.1.6.1.1.2
      vlans: 1.3.6.1.4.1.9.9.46.1.6.1.1.4
      vlans2k: 1.3.6.1.4.1.9.9.46.1.6.1.1.17
      vlans3k: 1.3.6.1.4.1.9.9.46.1.6.1.1.18
      vlans4k: 1.3.6.1.4.1.9.9.46.1.6.1.1.19
      native: 1.3.6.1.4.1.9.9.46.1.6.1.1.5
      status: 1.3.6.1.4.1.9.9.46.1.6.1.1.13
      encapsulation: 1.3.6.1.4.1.9.9.46.1.6.1.1.3
  vlans:
    table: 1.3.6.1.4.1.9.9.46.1.3.1
    name: 1.3.6.1.4.1.9.9.46.1.3.1.1.4.1
    dot1q_id: 1.3.6.1.4.1.9.9.46.1.3.1.1.6.1
    set:
      operation: 1.3.6.1.4.1.9.9.46.1.4.1.1.1
      row_status: 1.3.6.1.4.1.9.9.46.1.4.2.1.11.1
      type: 1.3.6.1.4.1.9.9.46.1.4.2.1.3.1
      name : 1.3.6.1.4.1.9.9.46.1.4.2.1.4.1
      said: 1.3.6.1.4.1.9.9.46.1.4.2.1.6.1
```