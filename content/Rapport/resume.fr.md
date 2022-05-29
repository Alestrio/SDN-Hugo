---
title: "Résumé"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport"]
weight: 1
---

## Résumé

Dans ce rapport, nous allons explorer la création d'une interface de communication pour les actifs réseau des salles de TP de l'IUT.
Cette interface sera un moyen de créer ou de modifier une infrastructure réseau de façon dynamique, en fonction des besoins du professeur.
Nous parlerons du contexte derrière le projet, c'est à dire de l'infrastructure déjà en place, des besoins qui nous ont mené à mener ce projet et des solutions possibles explorées.
Nous traiterons ensuite les différentes étapes de la création de l'interface, en commençant par la connexion entre l'api et le switch, puis de la conception de l'api en elle même, de la conception de l'interface web et de l'aspect de travail collaboratif.
Enfin, nous examinerons les améliorations envisageables, en commençant par la mise à jour de l'interface web en temps réel, puis la découverte automatique de l'infrastructure et l'instanciation auto d'apis, puis la prise en charge de switch de nouvelle génération, et enfin la création de graphique et d'alerte pour de la supervision.

## Mots clés

- __SDN - Software Defined Network__ : Concept de réseau défini par le logiciel. Cela permet une grande facilité de déploiement et de développement de l'infrastructure réseau.
- __Cisco__ : Fabricant d'actifs réseau, leader du marché.
- __API - Application Programming Interface__ : Interface de programmation d'application. C'est une interface de communication entre l'application et l'actif réseau.
- __SNMP - Simple Network Management Protocol__ : Protocole de supervision basée sur un système d'OIDs (Object Identifier).
- __Flask - Microframework Python__ : Framework de développement web basé sur Python. 
- __FastAPI__ : Framework de développement web basé sur Python. Permet de développer des APIs facilement et avec une documentation générée automatiquement.
- __Docker__ : Logiciel de déploiement de conteneurs. Permet de déployer des conteneurs sur des serveurs. Les conteneurs sont des applications qui fonctionnent dans un environnement complètemment isolé du reste du système. Cela permet une gestion sous forme d'unités indépendantes, de façon à pouvoir les gérer indépendamment.
- __GCP - Google Cloud Platform__ : Plateforme Cloud de Google. Ici, nous nous en servons comme plateforme d'hébergement de conteneurs.
- __Github__ : Plateforme de développement collaboratif. Permet de partager des codes, de créer des dépôts et de gérer des dépôts.
- __Hugo__ : Site de publication de contenus. Permet de générer des sites web statiques à partir de contenus écrits en Markdown.