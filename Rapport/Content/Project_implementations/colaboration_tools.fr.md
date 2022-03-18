---
title: "Outils de collaboration"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 2
---

Cette section est consacrée aux outils de collaboration que nous avons utilisé pendant la réalisation de notre projet.

## Hugo

Hugo est un générateur de **site web statique**, à partir de fichiers **Markdown**. Nous l'avons utilisé tout au long de ce projet pour créer une documentation pour le projet. De cette façon, nous avions par écrit, toutes les informations techniques concernant le projet, ce qui nous a permis de ne pas devoir dépendre continuellement de l'autre membre de l'équipe afin de comprendre et utiliser le travail réalisé.
C'est aussi l'outil que nous utilisons afin de créer ce rapport. L'ensemble des fichiers Markdown, sont hébergés sur GitHub, à cette adresse : https://github.com/Alestrio/SDN-Hugo

## Github

**[Github](../../../word_index/#github)** est une plateforme collaborative reposant sur **[Git](../../../word_index/#git)**, un utilitaire de gestion de version. Cette plateforme nous a permis de travailler chacun de notre côté sur nos tâches respectives, puis de **fusionner** les sources des deux membres de l'équipe. Ainsi, nous évitons les **conflits** de version, et nous avons un **historique** complet de toutes les versions du projet.
![contributions](/images/contributions.png) Contributions de l'équipe sur Github
![historique](/images/historique.png) Extrait d'historique du projet sur Github

Le **repository** (endroit où sont stockés les fichiers) est accessible à l'adresse : https://github.com/Alestrio/SDN-Cloudstack/

Afin de travailler chacun de notre côté sur nos tâches respectives, nous avons utilisé des **branches**. Une branche est l'équivalent d'un carrefour où une route se divise en plusieurs chemins.

Nous avons créé une branche backend, pour travailler sur tout ce qui concerne les APIs, puis une branche frontend, pour travailler sur tout ce qui concerne le gestionnaire de topologies et l'interface web. L'ensemble est ensuite intégré au projet en production, via la création d'une **Pull request**, qui permet de faire une demande de **fusion** entre deux branches. La branche **master** est ainsi la branche principale, et c'est celle qui est utilisée lors du déploiement automatique du projet.

![branches](/images/branches.png) Branches de travail sur Github

Dans un contexte de développement collaboratif avec une **production**, un service crucial qui doit être accessible constamment, la manière de s'organiser n'est pas tout à fait la même. Généralement, il y a trois branches principales : dev, preprod et prod. Dans le cas de Cloudstack, nous avons décidé de ne pas suivre cette architecture, puisque celle-ci est utilisée avec des équipes de dizaines de personnes. Étant deux, nous pouvions facilement nous contenter d'une branche par tâche, et de faire des Pull request ensuite.

## Trello

Afin de garder une trace sur les tâches faites/à faire, nous nous sommes aidés d'un outil appellé **Trello**. Cet outil est un outil de gestion de projet, qui permet de gérer les tâches, les priorités, les échéances, les tags, les membres, etc. Nous avons utilisé Trello pour gérer les tâches, et plusieurs colonnes : A faire, En cours, Fait, A regarder. Au fur et à mesure que nous avons travaillé sur nos tâches, nous avons ajouté des tâches dans les colonnes correspondantes, puis nous les avons fait passer dans les colonnes suivantes : En cours, Fait.
Cette façon d'organiser les choses s'appelle le **Kanban**.

![kanban](/images/kanban.png) Extrait de notre Kanban

## CI/CD

Afin de ne pas avoir à redéployer le projet manuellement à chaque modification, nous avons mis en place une **[CI/CD](../../../word_index/#cicd)**. CI/CD signifie **Continuous Integration/Continuous Deployment**. C'est une automatisation qui permet de lancer des tests à chaque modification sur un projet, mais aussi de le redéployer en production lors d'une modification sur une branche spéciale. Dans notre cas, c'est la branche **master**, qui est utilisée pour le déploiement automatique.

La machine virtuelle qui est utilisée pour le déploiement automatique est un serveur Ubuntu, qui est hébergé sur le datacenter de l'IUT. Sur cette machine, nous avons installé un **worker**, qui est un service qui permet de lancer les actions que nous avons définies dans le fichier .github/workflows/deploy_dc_chalons.yml. Ce fichier définit les actions à effectuer lors d'un déploiement automatique. Dans notre cas, voici les actions effectuées :

- **Pull** : permet de récupérer les modifications depuis le serveur de GitHub sur le serveur de déploiement.
- **Build** : permet de créer les images Docker pour le déploiement automatique.
- **Upload** : permet d'envoyer les images Docker sur l'hébergeur d'images (ici, Google Cloud, Artifact Registry).
- **Restart** : redémarre le Docker-Compose en production.

Une fois ces actions effectuées, la version en production est mise à jour.

Ce fichier est proposé en annexe 7.

## Google Cloud, Artifact Registry

Afin de stocker les images Docker, pour les récupérer sur n'importe quelle machine, nous utilisons **Google Artifact Registry**. C'est un service qui permet de stocker des images Docker. Il suffit ensuite de précisez l'adresse de l'image Docker pour la déployer.

![gcp_ar](/images/gcp_ar.jpg) Google Cloud, Artifact Registry
![gcp_prod](/images/gcp_prod.jpg) Déploiement sur serveur
