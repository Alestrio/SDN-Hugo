---
title: "Portail web"
date: 2021-03-12T09:21:34+02:00
draft: false
tags: ["rapport", "Project implementation"]
weight: 1
---

Le portail web est la partie en contact avec l'utilisateur. Elle doit permettre à l'utilisateur d'interagir avec le système.
Ce portail web est composé de plusieurs parties :

## Partie serveur : Flask
Cette partie est celle qui tourne sur le serveur. Elle gère les requêtes HTTP générées par l'utilisateur.
Cela veut dire que l'utilisateur peut accéder à des pages, qui sont générées par le serveur.
Le serveur qui met à disposition le portail web est appellé **Werkzeug**. Il s'agit du serveur integré au paquet **Flask**, de python. Ainsi, pour lancer le serveur, il suffit de lancer le script Python qui contient le point d'entrée du serveur.

La partie serveur repose aussi sur **Jinja2**, qui est un moteur de template. Il permet de générer des pages HTML à partir de templates. Les templates sont des fichiers HTML qui contiennent des instructions pour y intégrer des données de façon dynamique. (cf. Annexe 1)

La partie authentification est gérée par le module **flask-login**. Il permet de gérer les connexions de l'utilisateur. Les informations de connexion sont stockées dans un fichier [YAML](https://fr.wikipedia.org/wiki/YAML) qui est lu par le module **flask-login**.

La finalité de la partie serveur est de fournir les pages WEB à l'utilisateur, et de génerer les requêtes à l'interface logicielle (API) de l'actif à gérer en fonction des demandes de l'utilisateur. Concrètement, lorsque l'utilisateur veut changer un paramètre, il clique sur un bouton, et le serveur génère une requête HTTP qui est envoyée au module logiciel. Le module logiciel gère la modification du paramètre, et renvoie une réponse HTTP qui est envoyée au serveur. Le serveur renvoie la réponse à l'utilisateur. Ainsi, le serveur agit comme un intermédiaire entre l'utilisateur et le module logiciel, ce qui rend transparent l'utilisation du module logiciel.

## Partie client : Javascript
Cette partie est celle qui est gérée par le navigateur. Les **scripts** Javascript sont plutôt simples, et sont principalement dédiés à des fonctions de **transformation** de la page. Concrètement, il s'agit de la barre de navigation qui disparait et réapparait lorsque l'utilisateur clique sur un bouton, sur mobile, ou encore la configuration qui apparrait dans le champ de texte lorque l'utilisateur clique sur l'élément de configuration dans la partie "Configuration".
Cette partie est gardée volontairement simple, puisque le gros du travail est géré par le serveur Flask.

## État d'avancement
A ce jour, le portail web est en cours de développement.
Voici les fonctions qui sont actuellement implémentées :
- Connexion
- Déconnexion
- Résumé
- Création de configuration
- Modification de configuration
- Application de configuration
- Configuration "A la volée"

Il est possible d'ajouter la mise à jour automatique de la page Résumé lorsqu'un port change d'état (Branché, débranché). Cela permet de voir rapidement les changements de port. Cependant, par contrainte de temps, nous n'avons pas pu implémenter cette fonctionnalité. Nous y avons quand même pensé, et cela nous a permis de mettre au point le fonctionnement général et un exemple de code (cf Annexe 2).
Ci-dessous, un schéma du fonctionnement de cette fonctionnalité.
![maj_auto](/images/maj_auto.jpg)

