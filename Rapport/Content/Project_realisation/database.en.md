---
title: "Database"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 3
---

## Topology structure

Topologies are stored as strings in YAML format. The structure of this string is simple, it is composed of 4 parts:

- **name** : the name of the topology -> used to identify the topology instead of its ID, too heavy for the user
- **vlans** : the list of VLANs useful for the topology application, to be created if necessary
- **interfaces** : the list of interfaces configurations of the topology
- **trunks**: the list of trunk configurations of the topology

An example of topology is proposed in appendix 5

## How to save a topology

First of all, we had to make a choice regarding the storage technique of these data. We had several solutions:

- Store them as **YAML** files, in a specific folder on the server
- Store them in a **database**.

We chose the database option, but here again, we had many choices. During our course at the IUT, we studied the **PostGreSQL** database system, which is a relational system, meaning that the data are stored in tables, which are linked together. This imposes a rather **static** data format, not to mention the design of the database structure. So we started with a database able to store data in key/value format (JSON), **MongoDB**. MongoDB allows us to store our topologies almost as they are, without having to format them to fit into tables.
The advantage of this system is that **to an identifier, is linked a topology**, which is much simpler for the management of the database, but also for reading and writing in it.

## Interactions with the topology manager

When we started the project, we started with an API, managing all the operations related to the database, the assets, and the authentication. The system we developed does not involve direct communication between the database and the topology manager, but only with the API, which **interfaces** the database and the user interface part.
![diagramme_infra_ajd.jpg](/images/diagramme_infra_ajd.jpg)
The logic behind this choice was to get as close as possible to the architecture of software in production today.

Nevertheless, with hindsight and thanks to the discussions we had with our project tutor, we realized that we added **complexity** to the project, and that it would have been simpler to make the topology manager dialogue directly with the database. However, this choice is consistent with the choice to delegate the responsibility of applying topologies to the API. That's why we didn't backtrack and stayed with this architecture.

## User storage

Originally, users were also stored in the database. It was consulted by the API, which managed the authentication. This architecture was quite **complex**, so we decided not to keep it, since we realized again that we had **complexified** the project. So we decided to store the users in a YAML file, and to delegate the user connection to the topology manager. This also implies making the API open, without the need for authentication, but this is not a handicap, since in the end it will not be exposed.
