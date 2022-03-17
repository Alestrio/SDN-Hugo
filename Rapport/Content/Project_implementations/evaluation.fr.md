---
title: "Evaluation"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 3
---

Cette section est consacrée à notre évaluation objective et subjective du projet.

## Evaluation objective

### Par rapport au cahier des charges

Durant ce projet, nous avons pu développer un très grande majorité ($\approx 80%$) de ce qui était demandé dans le **cahier des charges**. Nous avons donc créé un système de configuration des actifs par **SNMP**. \
Nous avons aussi développé une **interface utilisateur** avec gestion des configurations préenregistrées, configuration à la volée et affichage des informations sur les actifs. \
Cette interface a été développée en gardant en tête que le principal objectif était de pouvoir utiliser ce système sur **mobile**.

## Hors du cahier des charges

Nous avons pu déployer notre projet en utilisant une infrastructure conteneurisée, à l'aide de **Docker** et Docker-Compose, ce qui nous a permis de nous rapprocher au maximum des nouvelles technologies de développement. \
Nous avons également utilisé un système de gestion de version **Git**, ce qui nous a permis de suivre les changements du code, et de mettre en place un système de déploiement automatique, aussi appellé CI/CD. \
Avec ce projet, nous avons aussi pu mettre en place une infrastructure de production complète, avec gestion de zone **DNS**, proxy **Traefik**, serveur web, serveur de bases de données **MongoDB**, etc. \

## Des tâches qui restent à faire

Une des fonctionnalités que nous n'avons pas pu mettre en place est la mise à jour automatique de l'affichage des informations sur les actifs. \
Nous avons néanmoins pu réfléchir au principe de base de cette fonctionnalité, et nous avions une idée assez précise de la mise en place de cette fonctionnalité. \
Il reste aussi du travail au niveau de l'interface web, dont on pourrait améliorer l'esthétique et la facilité d'utilisation.

## Evaluation subjective

### Compétences acquises

Grâce à ce projet, nous avons pu acquérir des compétences en système, à travers l'utilisation de technologies comme **Docker, Docker-Compose, SNMP, Traefik**, etc. \
Nous avons aussi pu acquérir des compétences en développement, à travers l'utilisation de technologies comme **Git, Github, et la CI/CD.** \
Enfin, nous avons pu acquérir des compétences en développement web, à travers l'utilisation de technologies comme **FastAPI, Flask,** etc.

### Des choix divergents par rapport au cahier des charges

Nous avons fait **deux choix majeurs** par rapport au cahier des charges. \
Tout d'abord, nous avions à la base choisi de gérer l'**authentification** et l'autorisation des utilisateurs, depuis l'**API**, qui aurait été le **centre nevralgique** de notre application. Ce choix s'est avéré trop **complexe** par rapport au cahier des charges, et nous a fait perdre un peu de temps pendant le développement de l'API et de l'interface web. \
Nous avons donc choisi de gérer l'authentification et l'autorisation des utilisateurs, depuis l'interface web, avec les identifiants et les mots de passes stockés dans un fichier de configuration. \
Le deuxième et dernier choix que nous avons fait, est de gérer les **interactions** avec la base de données et les actifs, uniquement à travers l'API. \
Ce choix a été fait pour nous rapprocher au maximum des techniques aujourd'hui en **production** dans une grande majorité d'applications web.