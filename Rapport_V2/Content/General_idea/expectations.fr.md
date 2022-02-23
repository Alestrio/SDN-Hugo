---
title: "Attentes du projet"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport"]
weight: 3
---

Le projet consiste à développer un outil permettant de gérer la **projection** des services dans les salles de TP.
Cet outil, de préférence sur une plateforme **mobile**, sera accessible par toutes les personnes disposant de l'accès au réseau de l'IUT via le service de tunnel **VPN** déjà en place.
Le placement dans les salles de TP d'un accès via **QR code** sera également possible, afin de faciliter l'accès au service.
Le changement de **topologie** devra être simple et rapide.
Ce que l'on appelle une topologie est un **ensemble de projections de services** sur des prises réseaux. Cela se manifeste par la modification de la configuration des prises réseaux dans les salles de TP. 
Les **paramètres** qui pourront varier sont multiples : mode de projection (accès à un seul service, envoi de plusieurs services (trunk)) et ports en fonctionnement.
Ces paramètres, afin de former une topologie, seront définis dans un texte de configuration, au format [YAML](https://fr.wikipedia.org/wiki/YAML), c'est à dire un fichier dont le contenu consiste en un assemblage de **couples clé/valeur**, facilement lisible et modifiable.
Exemple : `clé: valeur`
Cet outil devra proposer une méthode simple et graphique permettant **l'ajout, la modification et la suppression** des topologies, tout en permettant de **visualiser** les différentes projections.