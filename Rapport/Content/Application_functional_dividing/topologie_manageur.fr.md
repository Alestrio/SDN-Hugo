---
title: "Gestionnaire de topologie"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 3
---
Le gestionnaire de topologie est la pièce maitresse de notre projet, c'est la partie logiciel qui fait le lien entre le portail web, les actifs ainsi que la base de donnée.
Nous alons donc voir concrètement comment il fonctionne et pourquoi nous en avons besoin.

Aujourd'hui à l'IUT s'effectue de manière manuelle en utilisant des protocoles qui nécéssitent une intervention humaine (**[port console](../../../word_index/#port-console "port dédié à la configuration sur un équipement réseau")**, **[ssh](../word_index/#ssh "moyen de communication en réseau sécurisé")**, **[telnet](../../../word_index/#telnet "moyen de communication en réseau non sécurisé")**), cependant cela génère une dépendance humaine. Car même si ces méthodes permettent de modifier les configurations, cela requiert le chargement manuel d'un fichier, mais une fois de plus, cela induit une intervention humaine.

Pour palier à ce problème, les switchs les plus récents disposent d'interfaces de programmation logiciel, aussi appelé **[APIs](../../../word_index/#api "ensemble de fonction et de procédure créant une application")**, mais cette technologie n'est disponible que sur les modèle les plus récents et donc n'est pas accesible sur tous le **[parc d'actifs](../../../word_index/#parc-actifs "ensemble des équipements en productions sur un réseau")** de l'IUT.

Sur des modèles plus anciens, il est néanmoins possible de lire et de modifier des configurations en utilisant des outils de supervision.

Notre gestionnaire de topologies aura donc pour but de rendre compatible ces deux générations de matériel.

Pour cela nous avons donc envisagé de construire cette interface logiciel afin de permettre aux anciens modèles d'équipement tout comme aux plus récents d'être configurés depuis une seule et même interface.

Ce gestionnaire de topologies est également le pont entre notre portail web, l'API que bous développons et notre base de donnée car en effet c'est au travers de celui-ci que nous allons être capable de projeter et récupérer les topologies sur les actifs, grâce à une interface utilisateur Web.

![gestionnaire_de_topo.png](../../../../images/gestionnaire_de_topo.png)