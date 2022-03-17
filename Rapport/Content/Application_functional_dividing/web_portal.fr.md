---
title: "Le portail web"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 2
---

Le portail web est la partie visible du projet, c'est notre interface utilisateur.
Étant en contact avec l'utilisateur, notre interface doit donc être facile d'accès et facile d'utilisations.

L'accès à l'interface se fera donc de plusieurs façons pour la rendre la plus accesible. La première façon est via son url (www.sdn.chalons.univ-reims.fr).
La seconde est l'utilisation d'un QR Code placé dans les différentes salles de TP ainsi l'utilisateur aura juste à scanner le code pour arriver sur l'interface web où l'utilisateur devra s'identifier avant de choisir la topologie qu'il souhaite en fonction des critères vus précedement.

La gestion des droits et le système d'authentification est défini par un couple identifiant/mots de passe pour les étudiants et les professeurs. Ceux-ci ne sont pas individuels et sont sauvegardés dans un fichier de configuration.

L'interface en elle même, afin de rendre l'expérience utilisateur la plus simple et agréable possible, a été principalement développée pour fonctionner sur mobile. Cette interface se compose alors de quatres onglets.

Le premier onglet contiendra une vue "dashboard", qui est un résumé de la salle actuellement séléctionnée, on y trouvera par exemple le statut des actifs pour connaître leur état de fonctionnement.

Le second, "application de la configuration" est dédié à l'application de topologie. C'est sur cette page que l'on pourra choisir la topologie que l'on souhaite déployer ainsi que visualiser quelle topologie est actuellement en production.
 On pourra donc en sélectionnant la classe, le groupe et le TP, choisir la configuration adaptée et la mettre en production.

Le troisième onglet, "création de configuration" a lui pour but de créer les différentes configurations. Pour cela, on est ammené à sélectionner les différents **vlans**, **trunk** et **interfaces** que l'on peut alors configurer manuellement avant de sauvegarder cette configuration pour la déployer ultérieurement.

Le dernier onglet "configuration On The Go" a pour fonction d'activer et désactiver les différentes interfaces avec un clic. Cela permetra donc de facilement gérér le status des interfaces.
