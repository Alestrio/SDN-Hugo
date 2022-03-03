---
title: "Attentes du projet"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport"]
weight: 3
---

Le projet consiste à développer un outil permettant de gérer la **projection** des services dans les salles de TP.
Cet outil, de préférence sur une plateforme **mobile**, sera accessible par toutes les personnes disposant de l'accès au réseau de l'IUT via le service de tunnel **VPN** déjà en place.
L'accès au service pourra également se faire via un **QR Code**, affiché à l'entrée des salles de TP.
Le changement de **topologie** devra être simple et rapide.
Ce que l'on appelle une topologie est un **ensemble de projections de services** sur des prises réseaux. Cela se manifeste par la modification de la configuration des prises réseaux dans les salles de TP. 
Les **paramètres** qui pourront varier sont multiples : mode de projection du port (accès à un seul service, envoi de plusieurs services (trunk)) et mode de fonctionnement du port.
Ces paramètres, seront définis dans un fichier de configuration et formeront ainsi une topologie.
Ce projet devra comporter une partie de gestion des topologies, permettant, de façon simple, de créer, de modifier et de supprimer des topologies.
