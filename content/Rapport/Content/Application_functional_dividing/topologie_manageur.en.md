---
title: "Topology Manager"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 3
---

The topology manager is the key part of our project, it is the software part that makes the **link between the web portal, the assets and the database**.
We will see concretely how it works and why we need it.

Today, changing a configuration is done manually using protocols that require human intervention (**[port console](../../../word_index/#port-console "port dedicated to configuration on a network device")**, **[ssh](../../../word_index/#ssh "secure network communication method")**, **[telnet](../../../word_index/#telnet "non-secure network communication method")**), however this generates a human dependency. Even though these methods allow you to change configurations, it requires the intervention of a **authorized person**.

To overcome this problem, the most recent switches have software programming interfaces, also called **[APIs](../../../word_index/#api "set of functions and procedures creating an application")**, but this technology is only available on the most recent models and therefore is not available on all the **[asset pool](../../../word_index/#asset-pool "set of equipment in production on a network")** of the IUT.

On older models, it is nevertheless possible to read and modify configurations using **supervision tools**.

The goal of our topology manager will be to make these two generations of equipment **compatible**.

To do so, we have planned to build this software interface in order to allow the **old models** of equipment as well as the most recent ones to be configured from a single interface.

This topology manager is also the bridge between our web portal, the API that we are developing and our database because it is through it that we will be able to project and retrieve the topologies on the assets, thanks to a **Web** interface.
