---
title: "Web Portal"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 1
---

The web portal is the part in contact with the user. It must allow the user to interact with the system.
This web portal is composed of several parts:

## Server part: Flask

This part is the one that runs on the server. It manages the HTTP requests generated by the user.
This means that the user can access pages, which are generated by the server.
The server that provides the web portal is called **Werkzeug**. It is the server integrated in the **Flask** package of Python. So, to start the server, you just have to launch the Python script that contains the entry point of the server.

The server part is also based on **Jinja2**, which is a template engine. It allows to generate HTML pages from templates. Templates are HTML files which contain instructions to integrate data in a dynamic way. (see Appendix 1)

The authentication part is managed by the **flask-login** module. It allows to manage the user's connections. The connection information is stored in a [YAML] file (https://fr.wikipedia.org/wiki/YAML) which is read by the **flask-login** module.

The purpose of the server part is to provide WEB pages to the user, and to generate requests to the software interface (API) of the device to manage according to the user's requests. In concrete terms, when the user wants to change a parameter, he clicks on a button, and the server generates an HTTP request that is sent to the software module. The software module manages the modification of the parameter, and returns an HTTP response that is sent to the server. The server sends the response back to the user. Thus, the server acts as an intermediary between the user and the software module, which makes the use of the software module transparent.

## Client part : Javascript

This part is managed by the browser. Javascript **scripts** are rather simple, and are mainly dedicated to the **transformation** functions of the page. Concretely, it is the navigation bar that disappears and reappears when the user clicks on a button, on mobile, or the configuration that appears in the text field when the user clicks on the configuration item in the "Configuration" part.
This part is kept simple on purpose, since most of the work is handled by the Flask server.

## Status

At this time, the web portal is under development.
Here are the functions that are currently implemented:

- Login
- Logout
- Summary
- Configuration creation
- Configuration modification
- Configuration application
- On the fly" configuration

It is possible to add automatic update of the Summary page when a port changes state (Connected, Disconnected). This allows to quickly see the port changes. However, due to time constraints, we could not implement this feature. We still thought about it, and this allowed us to develop the general operation and a code example (see Appendix 2).
Below is a schematic of how this feature works.
![maj_auto](/images/maj_auto.jpg)