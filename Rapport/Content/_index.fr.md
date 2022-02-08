---
title: "Introduction"
date: 2022-01-27T17:07:28+02:00
weight: 4
chapter: true
---



Le SDN ou Software Defined Network est un concept dont le but est de créer ou modifier une infrastructure réseau de façon logicielle.
Sur les actifs de nouvelle génération, il est integré dans les systèmes d'exploitation des actifs réseau, sous forme d'une interface de communication, reposant sur des technologies de communication standards (HTTP).
Cette interface appellée API permet la configuration des actifs en envoyant des requêtes HTTP à l'API, c'est à dire, des requêtes similaires à celles utilisées par un navigateur.
Les actifs d'ancienne génération en production dans les salles de Travaux Pratiques, à l'IUT, sont dépourvus de cette interface. Il est donc nécessaire de créer une interface de communication pour les actifs réseau.

Ce constat nous ammène à la problématique suivante : __Comment adapter facilement la configuration des actifs réseau des salles de TP ?__

Nous commencerons tout d'abord par exposer le contexte derrière le projet, puis nous parlerons de la mise en oeuvre de l'interface de communication, pour finir par décrire les axes d'amélioration du projet.