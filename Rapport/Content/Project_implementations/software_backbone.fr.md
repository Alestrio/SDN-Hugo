---
title: "Ossature du logiciel"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "implementation"]
weight: 1
---

# Conteneurisation 

L'un des principes que nous avons tenu à mettre en place dans le cadre de notre projet est de conteneuriser nos applications.
La **conteneurisation** est une technique qui consiste à encapsuler des applications dans des unités indépendantes et isolées. Cela permet un déploiement rapide, et plus de sécurité.
Cela nous permet une plus grande modularité, puisque l'installation qui était autrefois fastidieuse, et qui impactait l'environnement du système, n'est plus nécessaire. Pour déployer une application, il suffit d'une seule commande, ou d'un bloc dans un fichier YAML.
Le paquet que nous utilisons est **Docker**, qui est un service de conteneurisation assez répandu.
Dans le cadre de notre projet, la conteneurisation a été mise en place, de façon à ce que tous les services nécessaires soient instantiables (peuvent être démarrés) d'une seule commande. Voici les services qui sont en production, et qui sont tous démarrés en tant que **conteneurs** :
- **DNS** : Un service BIND qui tourne avec les fichiers de configuration en lecture seule.
- **Base de données** : Une base de données MongoDB, avec les fichiers de la base dans un répertoire /home/mongo.
- **Serveur web** : Un serveur web pour la documentation (sur laquelle vous êtes), avec les fichiers HML générés par Hugo en lecture seule.
- **APIs** : Les APIs de l'application, déployées pour les salles Réseaux 1, 2 et 3, ainsi que pour un actif de test.
- **Gestionnaire de topologie** : Le gestionnaire de topologie développé pour le projet.
- **Traefik** : Le reverse proxy, permet de fournir le bon service, en fonction de l'URL demandée.

Pour démarrer ces services d'une seule commande, nous utilisons **Docker Compose**. Docker Compose est un outil qui permet de déployer des conteneurs, et de les configurer dans un fichier YAML. Le fichier YAML de configuration utilisé pour notre projet est proposé en annexe x.

# Traefik

Traefik est un **reverse proxy**, dont la spécificité est de découvrir les services à fournir depuis le service Docker.
Sa configuration se fait via des **tags** appliqués aux conteneurs, dans le fichier de Docker Compose. Via ces tags, nous pouvons configurer l'URL qui route sur le service, le port du service, et d'autres paramètres utiles pour un reverse proxy.
Traefik fournit aussi une interface web, qui permet de surveiller le bon fonctionnement du service.
![Traefik rp](/images/dashboard1.png)
Évidemment, le service de reverse proxy ne fonctionnerait pas pour un utilisateur, sans résolution de nom, il fonctionne donc en union avec le DNS.

# DNS et Délégation de zone

Le **DNS** permet de traduire des noms de domaine en adresses IP. Il est un des fondements d'Internet, et notre projet ne déroge pas à ce principe.
Dans le cadre de notre projet, plusieurs ressources nous ont été accordées :
- un enregistrement A : cloudstack.chalons.univ-reims.fr
- une délégation de zone : sdn.chalons.univ-reims.fr

Ces ressources ont été attribuées comme suit :
| Service | Adresse | Port |
| :--- | :--- | :--- |
| Interface de gestion Traefik | cloudstack.chalons.univ-reims.fr | 8080 |
| Documentation et rapport de projet | doc.sdn.chalons.univ-reims.fr | 80 |
| Gestionnaire de topologie et interface web | sdn.chalons.univ-reims.fr | 80 |
| APIs | R[123].api.sdn.chalons.univ-reims.fr | 80 |