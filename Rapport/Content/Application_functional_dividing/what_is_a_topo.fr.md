---
title: "Qu'est-ce que une topologie ?"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 1
---

L'intégralité de  ce projet ce base sur la capacité à déployer facilement des topologies varié sur les actifs réseaux. Nous allons donc voir ce qu'est une topologie et comment les définir.
Une topologie est donc un fichier de configuration que nous pouvons déployer sur les switchs. Ce fichier contiendra la configuration des différentes interfaces sous un format définit au préalable (json, yaml ...).
La configuration en elle même est composé des interfaces (**trunk**, **access** ou encore desactiver), on y trouve égallement les informations relative au différent **VLAN** (nom et numéro). La topologie sera donc un empillement de l'ensemble de ces informations.
La selection de la topologie ce fera par la suite au travers de l'interface web dans la quelle nous devrons définir les critères de choix de la topologie. Pour cela on ce base sur quatres critères principaux :
    - La salle de TP
    - La classe (RT1, RT2 ...)
    - Le groupe de TD/TP (TP1A, TP1B ...)
    - Le TP (TP wifi, TP téléphonie ...)
Basé sur ces quatres critères on pourra définir la topoplogie souhaité.
Une fois la topologie choisie elle sera traduite dans un format adapter pour les switchs par le gestionnaire de topologie.

Nous allons maintenant voir le fonctionnement du portail web.
