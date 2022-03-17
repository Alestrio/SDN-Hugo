---
title: "Gestionnaire de topologies"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 4
---

Le gestionnaire de topologies est l'élément central de notre projet. C'est lui qui fait le lien entre l'**utilisateur** via l'interface web, et les **actif réseaux** via l'**API**. C'est l'équivalent du contrôleur, dans les modèles de programmation MVC (Model-View-Controller).

## Interactions

Avant toute chose, l'utilisateur doit se **connecter** à l'interface web. Il se rend donc sur la page d'accueil du portail web. Il y trouve un bouton qui permet de se connecter. Une fois ses identifiants rentrés, l'appui sur le bouton de connexion envoie une requête au gestionnaire qui lui autorise ou non l'accès à l'interface de configuration.

Via l'interface web, l'utilisateur peut choisir la **topologie** qu'il souhaite déployer sur les actifs réseaux. Il s'agit d'une des tâches de ce gestionnaire. Concrètement, le gestionnaire vient demander à l'API les topologies disponibles, et les affiche dans une liste, dans l'onglet "**Configuration**". L'utilisateur peut alors choisir la topologie qu'il souhaite déployer sur les actifs réseaux. Une fois validée, le gestionnaire va demander à l'API de déployer la topologie choisie de façon **autonome**.

L'utilisateur peut aussi choisir de configurer l'actif **manuellement**. Il s'agit d'une autre tâche de ce gestionnaire. concrètement, il vient demander à l'API de l'actif, l'état de tous les ports, et les affiche dans une __liste en forme de switch__. L'utilisateur peut alors choisir les ports qu'il souhaite configurer, et changer les valeurs des paramètres. Une fois validée, le gestionnaire va demander à l'API de configurer l'actif, selon les consignes de l'utilisateur, de façon **unitaire**.

Une fonction, que nous n'avons pas encore développé, permettra de mettre à jour de façon **dynamique** l'affichage de l'interface lorsque un appareil est branché ou débranché sur un des ports du switch.

## Authentification

Comme dit précédemment, nous avions à la base, développé un système d'authentification au niveau de l'API, avec les couples identifiant/mot de passe stockés dans la base de données. Cependant, nous avons décidé de ne pas utiliser cette méthode, car elle était beaucoup trop compliquée par rapport au cahier des charges que nous avions. Nous avons donc décidé de créer un système d'authentification au niveau du gestionnaire, avec les identifiants/mot de passe stockés dans un fichier de configuration.
Cela nous donne donc deux comptes :
- Un compte administrateur, qui a les droits d'administration du gestionnaire : pour les enseignants.
- Un compte utilisateur, qui a les droits de lecture seule : pour les étudiants.

## Différences par rapport à ce qui a été pensé à la base

Au départ, il était prévu que le gestionnaire de topologie soit responsable de créer et appliquer les configurations sur les actifs, de façon unitaire. Concrètement, à partir des configurations, il devait demander à l'API d'effectuer les changements un par un sur les actifs. cependant, nous avons décidé de déléguer cette tâche à l'API. En effet, les latences inhérentes au protocole de supervision SNMP sont trop importantes pour un traitement unitaire, depuis un système externe à l'API. C'est donc elle qui gère l'application des configurations sur les actifs, en renvoyant les directives via **SNMP** lorsque celles-ci sont perdues. Si ces directives se perdent, c'est parce que SNMP est un protocole qui fonctionne sur UDP, donc en mode non-connecté. il n'y a donc pas de retour une fois la donnée envoyée (ACK en TCP). il faut donc contrôler que la configuration a bien été appliquée sur l'actif, et c'est l'API la mieux placée pour cela.