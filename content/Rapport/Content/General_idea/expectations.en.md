---
title: "Expectations of the project"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport"]
weight: 3
---

The project consists in developing a tool to manage the **projection** of services in the classrooms.
This tool, preferably on a **mobile** platform, will be accessible by all persons having access to the IUT network via the **VPN** tunnel service already in place.

It will also be possible to place a **QR code** access in the classrooms, in order to facilitate access to the service.
Changing the **topology** should be quick and easy.

A topology is a set of projections of services onto network outlets. This is manifested by changing the configuration of the network outlets in the classrooms. 
The **parameters** that can vary are multiple: projection mode (access to a single service, sending of several services (trunk)) and ports in operation.

These parameters, in order to form a topology, will be defined in a configuration text, in the [YAML] format (https://fr.wikipedia.org/wiki/YAML), that is to say a file whose content consists of an assembly of **key/value pairs**, easily readable and modifiable.
Example : `key: value`

This tool will have to propose a simple and graphical method for **adding, modifying and deleting** topologies, while allowing **visualizing** the different projections.


## Initial situation and prerequisites :
- Mr. BATISTE, professor at the IUT of Chalons-en-Champagne, teaches a wifi infrastructure module.
- The configuration of the network sockets is designed for a general use for most of the TP.
- This lab requires a specific configuration, to have access to the data-center services.
- The system is deployed on the data-center, and a QR code is displayed at the entrance of the lab rooms.

## What must be done to deploy a topology adapted to the needs of the lab?
- Mr. BATISTE, when he arrives in the lab room, connects to the VPN and scans the QR code.
- He arrives on the web interface linked to the infrastructure of the room.
- He connects, and arrives on a summary page.
- From there, he can choose the topology to use, and then apply it from the web interface.
- In the event that the chosen topology is not available, he can manually configure the network outlets.
- He can then save the topology he created.

