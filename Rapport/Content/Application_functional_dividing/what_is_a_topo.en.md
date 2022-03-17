---
title: "What is a Topology"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 1
---

The entire project is based on the ability to easily deploy various topologies on network devices. So we will see what a topology is and how to define them.

A topology is a configuration file that we can deploy on the switches. This file will contain the configuration of the different interfaces in a format defined beforehand ([JSON](../../../word_index/#json "file structure extension"), [YAML](../../../word_index/#yaml "file structure extension") ...).

The configuration itself, specifies the interface configurations (**[trunk](/word_index/#trunk "cisco port communication mode" )**, **[access](/word_index/#access "cisco port communication mode")** or disabled), there is also information on the various **[VLANs](/word_index/#vlan "Virtual bridge between two physically distant networks")** (names and numbers).
The topology is therefore a stack of all this information.

The selection of the topology will be done thereafter through the web interface in which we will have to define the criteria of choice of the topology.

For that we base ourselves on four main criteria:
- The class (RT1, RT2)
- The class (RT1, RT2 ...)
- The group of TD/TP (TP1A, TP1B ...)
- The TP (TP wifi, TP telephony ...)

Based on these four criteria we will be able to define the desired topology.

Once the topology is chosen, it will be translated into a format adapted for the network devices by the topology manager.