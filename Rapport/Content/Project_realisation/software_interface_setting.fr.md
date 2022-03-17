---
title: "Interface de configuration logicielle."
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 2
---

L'interface de configuration logicielle est un service permettant la configuration des actifs réseaux.

## Pourquoi cette interface ?
Tout d'abord, il est important de savoir comment les actifs réseaux sont configurés. Nous avons vu dans la section précédente qu'il était admis que nous n'utiliserions pas de protocoles interactifs comme le port Console ou le SSH (Console via réseau). Il a donc fallu trouver d'autres moyens. Nous nous sommes arrêtés sur l'utilisation d'un protocole bien connu dans le domaine de la supervision : le protocole **SNMP**. Il s'agit d'un protocole qui permet de communiquer avec tout type d'appareils (ordinateur, switch, routeur, etc.) afin de récupérer des informations, ou de pousser de la configuration.
Cette interface a donc pour but de traduire les actions SNMP en URL paramétrables. Cela permet une utilisation du protocole assez transparente et facile.

## Le protocole SNMP
Le protocole SNMP, basé sur **UDP**, est un protocole qui permet de communiquer avec des appareils pour récupérer des informations ou pousser de la configuration. Il utilise un système d'**OID** (Object Identifier) pour définir les informations que l'on souhaite récupérer. Un OID est un identifiant unique qui permet de définir un objet. Il est défini sous la forme d'une suite de chiffres, séparés par des points. Exemple d'OID : `1.3.6.1.2.1.1.5` (Permet de récupérer le nom d'hôte).
Les OIDs nécessaires pour notre interface sont définis dans le fichier de configuration de ce service (cf Annexe 3).

## Configuration obligatoire de l'actif réseau
Il est important de configurer l'actif réseau avant de pouvoir utiliser l'interface de configuration sur ce dernier. Voici les paramètres à configurer :
- **Interface SVI** : l'interface SVI de l'actif réseau. C'est une prise réseau virtuelle qui est utilisée pour configurer l'actif réseau.
- **Adresse IP** : l'adresse IP de l'actif réseau.
- **Communauté SNMP** : la communauté SNMP de l'actif réseau. C'est une valeur textuelle qui définit la clé de sécurité qui permet la configuration de l'actif réseau.

## Une API :
Puisque ce service traduit les actions SNMP en URL paramétrables, il s'agit d'une **API**. Une API est un serveur qui permet, via des URL, de récupérer des informations ou d'exécuter des actions. Dorénavant, nous ne parlerons plus d'"interface de configuration logicielle" mais d'**API**.
Une liste des toutes les URLs de l'API est disponible en Annexe 4.

## Construction de l'API
### Open API
Afin de nous rapprocher au maximum du côté "Terrain", nous avons décidé de construire notre API suivant le [**standard Open API**](https://www.openapis.org/). C'est un standard qui permet de définir des structures de données, et de ressources. Il définit des méthodes HTTP telles que GET, POST, PUT, DELETE. Ces méthodes ont toutes leurs fonctions. Par exemple, une requête GET permettra de récupérer des informations, et une requête POST permettra de pousser des informations.

Le paquet Python que nous utilisons pour construire notre API est [**FastAPI**](https://fastapi.tiangolo.com/). C'est un framework (Littéralement "Cadre de travail" -> Un ensemble d'outils) qui permet de construire rapidement une API. L'avantage de ce paquet, est qu'il génère automatiquement la documentation de l'API, en respectant le standard Open API.

### Support du SNMP en Python
L'utilisation du protocole SNMP en Python est prise en charge par deux paquets différents :
- **snmp-cmds** : Ce paquet est responsable de récupération de tables complètes (Table des interfaces, etc.) via le protocole SNMP. Il gère aussi toute la partie de poussée de configuration.
- **pysnmp** : Ce paquet prend en charge ce que le premier paquet ne peut pas. Il permet de récupérer des informations qui ne sont pas dans des tables.

### Le cache
La récupération initiale de toutes les données est très longue (environ 7 secondes), et cela est lié au fonctionnement même du protocole SNMP. Pour éviter de devoir récupérer les données à chaque fois, nous avons décidé de créer un **cache**. Ce cache est géré par le paquet Python [**Beaker**](https://beaker.readthedocs.io/en/latest/). Il s'agit d'un cache stocké en RAM, et qui permet de stocker des données pendant une durée définie. Ce paquet est tout indiqué par rapport au paquet **Redis**, car les informations stockées ont une taille définie qui ne bouge pas ou peu, on ne risque donc pas de dépassement de RAM. Redis, lui, est un cache beaucoup plus puissant, mais aussi beaucoup plus compliqué. Sa puissance aurait été énorme par rapport au travail qui lui aurait été demandé, donc il n'était pas rentable de l'utiliser.

### Authentification
Pendant le développement de notre API, nous somme partis sur une authentification au niveau de celle-ci. Cette authentification était basée sur une collection d'utilisateurs dans la base de données, avec un système de token [**JWT**](https://jwt.io/). Concrètement, l'utilisateur fournit un nom d'utilisateur et un mot de passe, et nous vérifions que ces informations sont correctes. Si elles sont correctes, nous générons un jeton, un code, qui doit être inclus dans les requêtes HTTP, pour celles qui sont protégées.

Cependant, avec le recul, nous nous sommes rendu compte que nous avions été chercher trop compliqué, puisque dans le cahier des charges, il était stipulé que l'API n'allait pas être **exposée**. Ainsi, l'authentification à ce niveau n'était pas nécessaire. Nous avons donc décidé de ne pas utiliser d'authentification, et de laisser l'ensemble de l'API **accessible**, sachant que seul le service de portail web aura accès à elle. L'authentification sera donc effectuée par le service de portail web, à partir d'infomations contenues dans le fichier de configuration de ce service.

## État d'avancement
A ce jour, on considère l'API comme terminée. Lors du développement de nouvelles fonctionnalités de l'interface web, il sera peut être nécessaire de la compléter, mais pour l'instant, l'API réalise les fonctions nécéssaires pour le bon fonctionnement du projet.