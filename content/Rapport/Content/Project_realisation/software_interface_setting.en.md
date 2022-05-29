---
title: "Software interface settings"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 2
---

The software configuration interface is a service allowing the configuration of network assets.

## Why this interface?

First of all, it is important to know how the network assets are configured. We saw in the previous section that it was assumed that we would not use interactive protocols such as the Console port or SSH (Console over Network). So we had to find other ways. We decided to use a well-known protocol in the field of supervision: the **[SNMP](../../../word_index/#snmp)** protocol. It is a protocol that allows to communicate with any kind of devices (computer, switch, router, etc.) in order to retrieve information, or to push the configuration.
The purpose of this interface is to translate SNMP actions into configurable URLs. This allows a transparent and easy use of the protocol.

## The SNMP protocol

The SNMP protocol, based on **[UDP](../../../word_index/#udp)**, is a protocol that allows to communicate with devices to retrieve information or push configuration. It uses a system of **OID** (Object Identifier) to define the information that we want to retrieve. An OID is a unique identifier that defines an object. It is defined in the form of a series of numbers, separated by dots. Example of OID : `1.3.6.1.2.1.1.5` (Used to retrieve the host name).
The OIDs required for our interface are defined in the configuration file for this service (see Appendix 3).

## Mandatory configuration of the network asset

It is important to configure the network asset before using the configuration interface on it. Here are the parameters to configure:

- **SVI interface**: the IVR interface of the network asset. This is a virtual network socket that is used to configure the network asset.
- **IP Address**: The IP address of the network asset.
- **SNMP Community**: The SNMP community of the network asset. This is a textual value that defines the security key that allows the configuration of the network asset.

## API:

Since this service translates SNMP actions into configurable URLs, it is an **API**. An API is a server that allows, via URLs, to retrieve information or execute actions. From now on, we will no longer speak of "software configuration interface" but of **API**.
A list of all the URLs of the API is available in Appendix 4.

## Building the API

### Open API

In order to get as close as possible to the "Field" side, we decided to build our API following the [**standard Open API**](https://www.openapis.org/). It is a standard that allows to define data and resource structures. It defines HTTP methods such as GET, POST, PUT, DELETE. These methods have all their functions. For example, a GET request will retrieve information, and a POST request will push information.

The Python package we use to build our API is [**FastAPI**](https://fastapi.tiangolo.com/). It is a framework (literally "Framework" -> A set of tools) that allows to quickly build an API. The advantage of this package is that it automatically generates the API documentation, respecting the Open API standard.

### SNMP support in Python

The use of SNMP protocol in Python is supported by two different packages:

- **snmp-cmds**: This package is responsible for retrieving complete tables (Interface table, etc.) via SNMP protocol. It also handles the whole configuration push part.
- **pysnmp**: This packet is responsible for doing what the first packet can't. It allows to retrieve information that is not in tables.

### The cache

The initial retrieval of all data is very long (about 7 seconds), and this is related to the way the SNMP protocol works. To avoid having to retrieve the data each time, we decided to create a **cache**. This cache is managed by the Python package [**Beaker**](https://beaker.readthedocs.io/en/latest/). It is a cache stored in RAM, and allows to store data for a defined time. This package is better than the **Redis** package, because the stored information has a defined size which does not move or does not move much, so there is no risk of RAM overflow. Redis is a much more powerful cache, but also much more complicated. Its power would have been enormous compared to the work that would have been asked of it, so it was not profitable to use it.

### Authentication

During the development of our API, we started with an authentication at the API level. This authentication was based on a collection of users in the database, with a token system [**JWT**](https://jwt.io/). In concrete terms, the user provides a username and a password, and we check that this information is correct. If they are correct, we generate a token, a code, that must be included in HTTP requests, for those that are protected.

However, in retrospect, we realized that we had been looking for too much complication, since in the specification, it was stipulated that the API was not going to be **exposed**. Thus, authentication at this level was not necessary. So we decided not to use authentication, and to leave the whole API **accessible**, knowing that only the web portal service will have access to it. The authentication will be done by the web portal service, from information contained in the configuration file of this service.

## Status

At this time, the API is considered complete. During the development of new functionalities of the web interface, it may be necessary to complete it, but for the moment, the API performs the functions necessary for the proper functioning of the project.