---
title: "Introduction"
date: 2022-01-27T17:07:28+02:00
weight: 4
draft: false
---


Le **SDN** ou **Software Defined Network** est un concept dont le but est de créer ou modifier une infrastructure réseau de façon logicielle.
Ce concept est un des sujets de projet qui nous ont été proposés par l'IUT de Châlons-en-Champagne, dans le cadre du projet de deuxième année de DUT Réseaux et Télécommunications.
Nous avons choisi ce sujet car il est très formateur et ouvre des perspectives d'acquisition de compétences dans un spectre très large, très utiles pour le développement d'un projet professionnel. Ce projet nous a aussi permis de développer des compétences en programmation, en supervision, en gestion de projet et réseaux. Nous espérons ainsi pouvoir utiliser ces compétences dans notre future carrière.

Sur les actifs de nouvelle génération, le concept de SDN est integré dans les systèmes d'exploitation des actifs réseau, sous forme d'une **interface de communication**, reposant sur des technologies de communication standards (HTTP).
Cette interface appellée **API** pour Application programming Interface, permet la configuration des actifs en envoyant des requêtes HTTP à l'API, c'est à dire, des requêtes similaires à celles utilisées par un navigateur web.
Les actifs d'ancienne génération en production dans les salles de Travaux Pratiques, à l'IUT, sont dépourvus de cette interface. Il est donc nécessaire de **créer une interface de communication** pour ces actifs réseaux.

Ce constat nous ammène à la problématique suivante : __Comment adapter facilement la configuration des actifs réseau des salles de TP ?__

Nous commencerons tout d'abord par exposer certaines **généralités** concernant le projet, puis nous parlerons plus généralement du **découpage fonctionnel** de notre application. Nous enchainerons ensuite sur deux parties plus techniques concernant la **réalisation** du projet et sa mise en œuvre en **production**.