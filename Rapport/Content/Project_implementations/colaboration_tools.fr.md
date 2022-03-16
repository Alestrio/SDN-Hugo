---
title: "Outils de collaboration"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 2
---

Cette section est consacrée aux outils de collaboration que nous avons utilisé pendant la réalisation de notre projet.

## Hugo

Hugo est un générateur de site web statique, à partir de fichiers Markdown. Nous l'avons utilisé tout au long de ce projet pour créer une documentation pour le projet. De cette façon, nous avions par écrit, toutes les informations techniques concernant le projet, ce que nous a permis de ne pas devoir dépendre continuellement de l'autre memebre de l'équiê afin de comprendre et utiliser le travail réalisé.
C'est aussi l'outil que nous utilisons afin de créer ce rapport. L'ensemble des fichiers Markdown, sont hébergés sur GitHub, à cette adresse : https://github.com/Alestrio/SDN-Hugo

## Github

Github est une plateforme collaborative reposant sur Git, un utilitaire de gestion de version. Cette plateforme nous a permis de travailler chacun de notre côté sur nos tâches respectives, puis de fusionner les sources des deux membres de l'équipe. Ainsi, nous évitons les conflits de version, et nous avons un historique complet de toutes les versions du projet. 
![contributions](/images/contributions.png) Contributions de l'équipe sur Github
![historique](/images/historique.png) Extrait d'historique du projet sur Github

Le repo (endroit où sont stockés les fichiers) est accessible à l'adresse : https://github.com/Alestrio/SDN-Cloudstack/

Afin de travailler chacun de notre côté sur nos tâches respectives, nous avons utilisé des branches. Une branche est l'équivalent d'un carrefour où une route se divise en plusieurs chemins. Nous avons créé une branche backend, pour travailler sur tout ce qui concerne les APIs, puis une branche frontend, pour travailler sur tout ce qui concerne le gestionnaire de topologies et l'interface web. l'ensemble est ensuite intégré au projet en production, via la création d'une Pull request, qui permet de faire une demande de fusion entre deux branches. La branche main est ainsi la branche principale, et c'est celle qui est utilisée lors du déploiement automatique du projet.

![branches](/images/branches.png) Branches de travail sur Github

Dans un contexte de développement collaboratif avec une production, un service crucial qui doit être accessible constamment, la manière de s'organiser n'est pas tout à fait la même. Généralement, il y a trois branches principales : dev, preprod et prod. Dans le cas de Cloudstack, nous avons décidé de ne pas suivre cette architecture, puisque celle-ci est utilisée avec des équipes de dizaines de personnes. Étant deux, nous pouvions facilement nous contenter d'une branche par tâche, et de faire des Pull request ensuite.

## Trello

Afin de garder une trace sur les tâches faites/à faire, nous nous sommes aidés d'un outil appellé Trello. Cet outil est un outil de gestion de projet, qui permet de gérer les tâches, les priorités, les échéances, les tags, les membres, etc. Nous avons utilisé Trello pour gérer les tâches, et plusieurs colonnes : A faire, En cours, Fait, A regarder. Au fur et à mesure que nous avons travaillé sur nos tâches, nous avons ajouté des tâches dans les colonnes correspondantes, puis nous les avons fait passer dans les colonnes suivantes : En cours, Fait.
Cette façon d'organiser les choses s'appelle le Kanban.

![kanban](/images/kanban.png) Extrait de notre Kanban

## CI/CD


