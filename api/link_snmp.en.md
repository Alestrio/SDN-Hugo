---
title: "SNMP/API link".
date: 2021-10-17T12:42:10Z
tags: ["notice", "api", "snmp"]
draft: false
---

To communicate with the assets, the API uses the SNMP protocol. You can find more information about the protocol on the dedicated research page. This article discusses the use of this protocol with the API.

## Basic libraries:

Initially, to design our API, we used __PySNMP__. It is a high level library entirely made with Python allowing to use the SNMP protocol with the Python language. 

It is possible to do any SNMP action with this library, however, it has several drawbacks:
- The syntax is heavy and repetitive
- Due to its design, it brings a lot of latency for the processing of large volumes of information

To solve the first problem, we have, in collaboration with Alexandre GOSSARD and Corentin FREIRE from the AC-VISION project, created a class, __SNMPUtils__, to simplify the syntax when using this library, but this does not solve the second problem : latency...

In order to solve this second problem, we looked for several solutions:
- Concurrent information retrieval (using several processes (thread) at the same time)
- Modification of the process of treatment of the information in order to gain in cpu time
- Use of a lower level library

This last solution was chosen, using the __snmp_cmds__ library, which is based on the __net_snmp__ binary, present natively on Linux systems, and easily installed on Windows systems. \
This library allows the recovery of complete tables, in a time very close to that of the __net_snmp__ binary ($\approx$ 0.7s). It saves a lot of time. Its disadvantage is that it does not know how to handle bytes-strings, which makes the use of __PySNMP__ mandatory in these cases. So we use our SNMPUtils class in order to reconcile the two libraries in a common and understandable base.

## The SwitchOperations class

In order to respect the following programming principles :
- DRY : Don't Repeat Yourself
- Modularity and responsibility management

we use a class to create an abstraction layer between the SNMP part and the API part. \
This class is only responsible for the retrieval and transmission of configuration with the asset, and allows the API code to remain understandable and concise. Thus, the responsibility of the actions with the asset is given to this class, which allows to be more efficient in maintenance and a better understanding of the code.

As the retrieval of information from the asset remains slow, despite the use of the solutions described above, this class also handles the __caching__ and rebuilding of the cache. This saves a lot of time for the user, while being totally transparent since the cache is automatically regenerated at each configuration change. \
For the retrieval of all the information available via the API, we go from 12s to about 1.1s.

The management of the cache is delegated by this class to the __Beaker__ library, and it is a cache in RAM, with an expiration of 10mn.