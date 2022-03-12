---
title: "Gestionnaire de topologie"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 3
---

Le gestionnaire de topologie est la colonne vertébrale de notre projet, c'est la partie logicielle qui fait le lien entre le portail web, et l'interface de configuration logicielle.
Nous allons donc voir concrètement comment il fonctionne et pourquoi nous en avons besoin.

Aujourd'hui à l'IUT s'effectue de manière manuelle en utilisant des protocoles qui nécéssitent une intervention humaine (port console, **ssh**, **telnet**), cependant cela génère une dépendance envers les personne abilitées.
Pour palier ce promblème, les actifs les plus récent disposent d'interfaces de programmation logiciel, aussi appelées **API**, mais cette technologie n'est disponible que sur les modèles les plus récents et donc n'est pas accesible sur tous les actifs du parc.
Sur des modèles plus anciens, il est néanmoins possible de lire et de modifier des configuration en utilisant des protocoles de supervision.
Notre gestionnaire de topologie aura donc pour but de rendre compatibles ces deux générations de matériel. Pour cela nous avons envisagé de construire cette interface logiciel afin de pouvoir configurer les deux générations d'actifs en même temps.
Ce gestionnaire de topologie va permettre à l'utilisateur de choisir la topologie qu'il souhaite déployer, de voir simplement quelle topologie est actuellement en production, et de configurer les différents actifs.
