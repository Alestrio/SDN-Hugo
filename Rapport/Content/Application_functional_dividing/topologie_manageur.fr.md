---
title: "Gestionnaire de topologie"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 3
---

Le gestionnaire de topologie est le **backbone** de notre projet, c'est la partie logiciel qui fait le lien entre le portail web, les actifs ainsi que la base de donnée.
Nous alons donc voir concrètement comment il fonctionne et pourquoi nous en avons besoin.

Aujourd'hui à l'IUT s'éfectue de manière manuelle en utilisant des protocoles qui nécéssite une intervention humaine (port console, **ssh**, **telnet**), cependant cela génère une dépéndance humaine et limite donc la modularité des actifs. Car même si ces méthodes permettent de modifier les configurations, cela requiert le chargement manuellement d'un fichier, mais une fois de plus, cela induit une intervention humaine.
Pour palier à ce promblème, les switchs les plus récent dispose d'interface de programmation logiciel, aussi appelé **api**, mais cette tèchnologie n'est disponible que sur les plus récent modèle et donc n'est pas accesible sur tous les **parc réseaux**.
Sur des modèles plus anciens, il est néanmoins possible de lire et de modifier des configuration en utilisant des outils de supervisions.
Notre gestionnaire de topologie aura donc pour but de rentre compatible ces deux générations de matériel. Pour cela nous avons donc envisagé de construire cette interface logiciel afin de permetre au anciens modeles d'equipement touts comme au plus récent d'être configuerer depuis une seul et même interface.
Cette gestionnaire de topologie est égallment le pont entre notre portail web, nos switchs et notre base de donnée car en effect c'est au travers de celui-ci que nous allons être capable de projeté et récupérer les topologies sur les actifs depuis le portail web.

Nous alons dans cette dernieres section voir 