---
title: "Lien SNMP/API"
date: 2021-10-17T12:42:10Z
tags: ["notice","api", "snmp"]
draft: false
---

Pour communiquer avec les actifs, l'API utilise le protocole SNMP. Vous pourrez trouver plus d'information sur le protocole sur la page dédiée des recherches. Cet article traite de l'utilisation de ce protocole avec l'API.

## Bibliothèques de base :

Au départ, pour concevoir notre API, nous avons utilisé __PySNMP__. Il s'agit d'une bibliothèque de haut niveau entièrement faite avec Python permettant d'utiliser le protocole SNMP avec le langage Python. 

Il est possible de faire n'importe quelle action SNMP avec cette bibliothèque, cependant, elle présente plusieurs inconvénients :
- La syntaxe est lourde et répétitive
- De part sa conception, elle apporte beaucoup de latence pour le traitement de gros volumes d'informations

Pour palier le premier problème, nous avons, en collaboration avec Alexandre GOSSARD et Corentin FREIRE du projet AC-VISION, créé une classe, __SNMPUtils__, pour simplifier la syntaxe lors de l'utilisation de cette bibliothèque, mais cela ne règle pas le second problème la latence...

Afin de palier ce second problème, nous avons recherché plusieurs solutions :
- Récupération d'informations concurentielle (En utilisant plusieurs processus (thread) en même temps)
- Modification du processus de traitement des informations afin de gagner en temps de processeur
- Utilisation d'une bibliothèque de plus bas niveau

C'est cette dernière solution qui a été retenue, en utilisant la bibliothèque __snmp_cmds__, qui repose sur le binaire __net_snmp__, présent nativement sur les systèmes linux, et installable facilement sur les systèmes Windows. \
Cette bibliothèque permet la récupération de tables complètes, en un temps très proche de celui du binaire __net_snmp__ ($\approx$ 0.7s). Et permet donc de gagner énormément de temps. Son inconvénient est qu'elle ne sait pas traiter les octet-strings, ce qui rend obligatoire l'utilisation de __PySNMP__ dans ces cas. Nous utilisons donc notre classe SNMPUtils afin de concilier les deux librairies en une base commune et compréhensible.

## La classe SwitchOperations

Afin de respecter les principes de programmation suivants :
- DRY : Don't Repeat Yourself
- Modularité et gestion de responsabilité

nous utilisons une classe pour créer une couche d'abstraction entre la partie SNMP et la partie API. \
Cette classe est responsable uniquement de la récupération et transmission de configuration avec l'actif, et permet au code de l'API de rester compréhensible et concis. Ainsi, la responsabilité des actions avec l'actif est donnée à cette classe, ce qui permet d'être plus efficace en maintenance et une meilleure compréhension du code.

La récupération des informations de l'actif restant lente, malgré l'utilisation des solutions décrites ci-dessus, cette classe gère aussi la mise en __cache__ et la reconstruction du cache. Cela permet un gain de temps énorme pour l'utilisateur, tout en étant totalement transparent puisque le cache est regénéré automatiquement à chaque changement de configuration. \
Pour la récupération de l'ensemble des informations disponibles via l'API, on passe ainsi de 12s, à environ 1.1s.

La gestion du cache est déléguée par cette classe à la bibliothèque __Beaker__, et il s'agit d'un cache en mémoire vive, avec une expiration de 10mn.