---
title: "Topologie manager"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 4
---

The topology manager is the central element of our project. It is the link between the **user** via the web interface, and the **network agents** via the **API**. It is the equivalent of the controller, in the MVC (Model-View-Controller) programming models.

## Interactions

First of all, the user must **connect** to the web interface. He therefore goes to the home page of the web portal. There he finds a button that allows him to connect. Once the user has entered his credentials, pressing the login button sends a request to the manager who authorizes or not the access to the configuration interface.

Via the web interface, the user can choose the **topology** he wants to deploy on the network devices. This is one of the tasks of this manager. Concretely, the manager comes to ask the API for the available topologies, and displays them in a list, in the "**Configuration**" tab. The user can then choose the topology he wants to deploy on the network devices. Once validated, the manager will ask the API to deploy the chosen topology in an **autonomous** way.

The user can also choose to configure the device **manually**. This is another task of this manager. Specifically, it asks the API of the device for the status of all ports, and displays them in a __list in switch form__. The user can then choose the ports he wants to configure, and change the values of the parameters. Once validated, the manager will ask the API to configure the device, according to the user's instructions, in a **unitary** way.

A function, which we have not yet developed, will allow the interface display to be updated **dynamically** when a device is plugged or unplugged on one of the switch ports.

## Authentication

As said before, we had originally developed an authentication system at the API level, with the login/password pairs stored in the database. However, we decided not to use this method, because it was much too complicated compared to the specifications we had. So we decided to create an authentication system at the manager level, with the login/password stored in a configuration file.
This gives us two accounts:

- An **administrator** account, which has administrator rights for the manager: for teachers.
- A **user** account, which has read-only rights: for students.

## Differences from what was originally thought

At the beginning, it was planned that the topology manager would be responsible for creating and applying the configurations on the devices, in a unitary way. Concretely, from the configurations, he had to ask the API to make the changes one by one on the devices. However, we decided to delegate this task to the API. Indeed, the **latencies** inherent to the SNMP supervision protocol are too important for a unitary treatment, from a system external to the API. It is therefore the API that manages the application of the configurations on the devices, by returning the directives via **SNMP** when they are lost. If these directives are lost, it is because SNMP is a protocol which works on UDP, thus in non-connected mode. There is thus no return once the data is sent (ACK in TCP). it is thus necessary to control that the configuration was well applied on the devices, and it is the API who does that.
