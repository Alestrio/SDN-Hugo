---
title: "web portal"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 2
---

The **web portal** is the visible part of the project, it is our user interface.
Being in contact with the user, our interface must be **easy to access** and easy to use.

The access to the interface will be done in several ways to make it as accessible as possible. The first way is via its URL (www.sdn.chalons.univ-reims.fr).
The second way is by using a **QR Code** placed in the different classrooms so the user will just have to scan the code to get to the web interface where the user will have to identify himself before choosing the topology he wants to deploy.

The rights management and authentication system is defined by a pair of login/passwords for students and teachers. These are not individual and are saved in a configuration file.

The interface itself, in order to make the user experience as simple and pleasant as possible, has been mainly developed to work on **mobile**. This interface is composed of four tabs.

The first tab will contain a "dashboard" view, which is a **summary** of the room currently selected, we will find for example the status of the devices to know their operating status.

The second, "configuration application" is dedicated to the topology application. On this page we can choose the topology we want to deploy and see which topology is currently in production.
By selecting the class, the group and the TP, you can choose the appropriate configuration and put it into production.

The third tab, "configuration creation" is used to create the different configurations. To do this, we are led to select the different **vlans**, **trunk** and **interfaces** that we can then configure manually before saving this configuration to deploy it later.

The last tab "On The Go configuration" has the function to activate and deactivate the different interfaces with a click. This will allow to easily manage the status of the interfaces.
