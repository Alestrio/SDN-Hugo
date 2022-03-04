---
title: "Expectations of the project"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport"]
weight: 3
---

The project consists of developing a tool to manage the **projection** of services in the classrooms.
This tool, preferably on a **mobile** platform, will be accessible by all persons with access to the IUT network via the **VPN** tunnel service already in place.
It will also be possible to place a **QR code** access in the classrooms, in order to facilitate access to the service.
Changing the **topology** should be quick and easy.
A topology is a **set of service projections** on network sockets. This is manifested by changing the configuration of the network outlets in the workstations. 
The **parameters** that may vary are multiple: mode of projection (access to a single service, sending several services (trunk)) and ports in operation.
These parameters, in order to form a topology, will be defined in a configuration text, in [YAML](https://fr.wikipedia.org/wiki/YAML) format, i.e. a file whose content consists of an assembly of **key/value pairs**, easily readable and modifiable.
Example: `key: value`
This tool should provide a simple and graphical method for **adding, modifying and deleting** topologies, while allowing **viewing** the different projections.
