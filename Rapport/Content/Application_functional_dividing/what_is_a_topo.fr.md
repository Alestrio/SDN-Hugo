---
title: "Qu'est-ce que une topologie ?"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 1
---

L'intégralité de ce projet se base sur la capacité à déployer facilement des topologies variées sur les actifs réseaux. Nous allons donc voir ce qu'est une topologie et comment les définir.
Une topologie est donc un fichier qui résume une configuration que nous pouvons déployer sur les switchs. Ce fichier contient la configuration des différentes interfaces sous la forme d'un empilement de clés/valeurs.
La sélection de la topologie se fera par le biais de l'interface web dans laquelle nous devrons définir les critères de choix de la topologie. Pour cela on se base sur quatres critères principaux :
- La salle de TP
- La classe (RT1, RT2 ...)
- Le groupe de TD/TP (TP1A, TP1B ...)
- Le TP (TP wifi, TP téléphonie ...)