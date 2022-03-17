---
title: "Qu'est-ce que une topologie ?"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 1
---

L'intégralité de  ce projet se base sur la capacité à déployer facilement des topologies variées sur les actifs réseaux. Nous allons donc voir ce qu'est une topologie et comment les définir.

Une topologie est donc un fichier de configuration que nous pouvons déployer sur les switchs. Ce fichier contiendra la configuration des différentes interfaces sous un format défini au préalable ([JSON](../word_index/#json "extension de structure de fichier"), [YAML](../word_index/#yaml "extension de structure de fichier") ...).

La configuration en elle même, spécifie les configurations d'interfaces(**[trunk](../word_index/#trunk "mode de communication de port cisco" )**, **[access](../word_index/#access "mode de communication de port cisco")** ou encore désactivée), on y trouve également les informations relatives aux différents **[vlan](../word_index/#vlan "reseau virtuel crée dans un réseau pour connecter des équipements à différentes locations")** (noms et numéros).
La topologie est donc un empilement de l'ensemble de ces informations.

La sélection de la topologie se fera par la suite au travers de l'interface web dans laquelle nous devrons définir les critères de choix de la topologie.

Pour cela on se base sur quatre critères principaux :
    - La salle de TP
    - La classe (RT1, RT2 ...)
    - Le groupe de TD/TP (TP1A, TP1B ...)
    - Le TP (TP wifi, TP téléphonie ...)
Basé sur ces quatres critères on pourra définir la topoplogie souhaité.

Une fois la topologie choisie elle sera traduite dans un format adapté pour les switchs par le gestionnaire de topologie.
