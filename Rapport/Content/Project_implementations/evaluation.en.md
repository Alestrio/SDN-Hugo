---
title: "Evaluation"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 3
---

This section is devoted to our objective and subjective evaluation of the project.

## Objective evaluation

### In relation to the specifications

During this project, we were able to develop a very large majority (\approx 80%) of what was requested in the **specification**. We have therefore created a system of device configuration by **SNMP**. \
We also developed a **user interface** with management of pre-saved configurations, on-the-fly configuration and display of information on the devices. \
This interface was developed keeping in mind that the main objective was to be able to use this system on **mobile**.

## Out of specification

We were able to deploy our project using a containerized infrastructure, using **Docker** and Docker-Compose, which allowed us to get as close as possible to the new development technologies. \
We also used a **Git** version management system, which allowed us to track changes in the code, and to set up an automatic deployment system, also called CI/CD. \
With this project, we were also able to set up a complete production infrastructure, with **DNS** zone management, **Traefik** proxy, web server, **MongoDB** database server, etc.

## Tasks that remain to be done

One of the features that we have not been able to implement is the automatic update of the devices information display. \
Nevertheless, we were able to think about the basic principle of this functionality, and we had a fairly precise idea of how to implement it. \
There is also work to be done on the web interface, which could be improved in terms of aesthetics and ease of use.

## Subjective evaluation

### Skills acquired

Thanks to this project, we were able to acquire system skills, through the use of technologies like **Docker, Docker-Compose, SNMP, Traefik**, etc. \
We were also able to acquire development skills, through the use of technologies such as **Git, Github, and CI/CD.** \
Finally, we were able to acquire web development skills, through the use of technologies like **FastAPI, Flask,** etc.

### Choices that diverge from the specifications

We made **two major choices** in relation to the specifications. \
First of all, we had originally chosen to manage the **authentication** and authorization of users, from the **API**, which would have been the **center of gravity** of our application. This choice turned out to be too **complex** compared to the specifications, and made us lose some time during the development of the API and the web interface. \
We therefore chose to manage the authentication and authorization of users from the web interface, with identifiers and passwords stored in a configuration file. \
The second and final choice we made was to manage interactions with the database and devices, only through the API. \
This choice was made to get as close as possible to the techniques used today in **production** in the vast majority of web applications.