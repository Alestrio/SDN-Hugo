---
title: "Colaboration tools"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 2
---

This section is dedicated to the collaboration tools we used during the realization of our project.

## Hugo

Hugo is a **static website** generator, based on **Markdown** files. We used it throughout this project to create a documentation for the project. This way, we had in text, all the technical information about the project, which allowed us not to have to depend continuously on the other team member to understand and use the work done.
This is also the tool we use to create this report. All the Markdown files are hosted on GitHub, at this address: https://github.com/Alestrio/SDN-Hugo

## Github

**[Github](../../../word_index/#github)** is a collaborative platform based on **[Git](../../../word_index/#gi)**, a version management utility. This platform allowed us to work each on our own on our respective tasks, then to **merge** the sources of both team members. This way, we avoid version **conflicts**, and we have a complete **history** of all versions of the project.
![contributions](/images/contributions.png) Team contributions on Github
![historique](/images/historique.png) Extract of the project history on Github

The **repository** (place where the files are stored) is accessible at : https://github.com/Alestrio/SDN-Cloudstack/

In order to work on our respective tasks, we used **branches**. A branch is the equivalent of a crossroads where a road divides into several paths.

We created a backend branch, to work on everything related to the APIs, then a frontend branch, to work on everything related to the topology manager and the web interface. The whole thing is then integrated into the project in production, via the creation of a **Pull request**, which allows to make a **merge** request between two branches. The **master** branch is then the main branch, and it is the one used during the automatic deployment of the project.

![branches](/images/branches.png) Working branches on Github

In a collaborative development context with a **production**, a crucial service that must be constantly accessible, the way of organizing is not quite the same. Generally, there are three main branches: dev, preprod and prod. In the case of Cloudstack, we decided not to follow this architecture, since it is used with teams of dozens of people. Being two, we could easily settle for one branch per task, and then make Pull requests.

## Trello

In order to keep track of the tasks done/to be done, we used a tool called **Trello**. This tool is a project management tool, which allows to manage tasks, priorities, deadlines, tags, members, etc. We used Trello to manage the tasks, and several columns: To do, In progress, Done, To look at. As we worked on our tasks, we added tasks to the corresponding columns, then moved them to the next columns: In Progress, Done.
This way of organizing things is called **Kanban**.

![kanban](/images/kanban.png) Extract of our Kanban

## CI/CD

In order not to have to manually redeploy the project every time we make a change, we set up a **[CI/CD](../../../word_index/#cicd)**. CI/CD stands for **Continuous Integration/Continuous Deployment**. It is an automation that allows to launch tests at each modification on a project, but also to redeploy it in production at the time of a modification on a special branch. In our case, it is the **master** branch, which is used for the automatic deployment.

The virtual machine that is used for the automatic deployment is an Ubuntu server, which is hosted on the datacenter of the IUT. On this machine, we have installed a **worker**, which is a service that allows to launch the actions that we have defined in the .github/workflows/deploy_dc_chalons.yml file. This file defines the actions to be performed during an automatic deployment. In our case, here are the actions performed:

- **Pull**: allows to retrieve the changes from the GitHub server on the deployment server.
- **Build**: create the Docker images for the automatic deployment.
- **Upload**: allows to send the Docker images to the image host (here Google Cloud, Artifact Registry).
- **Restart**: restarts the Docker-Compose in production.

Once these actions are done, the production version is updated.

This file is proposed in appendix 7.

## Google Cloud, Artifact Registry

In order to store the Docker images, to retrieve them on any machine, we use **Google Artifact Registry**. It is a service that allows to store Docker images. Then you just have to specify the address of the Docker image to deploy it.

![gcp_ar](/images/gcp_ar.jpg) Google Cloud, Artifact Registry
![gcp_prod](/images/gcp_prod.jpg) Deployment on server