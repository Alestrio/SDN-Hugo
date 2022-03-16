---
title: "Le portail web"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "AFD"]
weight: 2
---

Le portail web est la partie visible du projet, c'est notre interface utilisateur.
Etant en contact avec l'utilisateur, notre interface dois donc être facile d'acces et facile d'utilisation.
L'acces à l'interface ce fera donc de plusieur façon pour la rendre la plus accesible. La première façon est via son url (www.sdn.chalons.univ-reims.fr). La second est l'utilisation d'un QR Code placé dans les différentes salles de TP ainsi l'utilisateur aura juste à scanné le Code pour arrivé sur l'interface web ou l'utilisateur devra s'identifier avant de choisir la topologie qu'il souhaite en fonction des critères vue précedement.

La gestion des droits et le système d'authetification est défini par un couple identifiant/mots de passe pour les étudiants et les profésseurs. Ceux ci ne sont pas individuelle et sont sauvegarder dans un fichier de configuration. Ce choix à été réaliser en replacement du système précedent qui voulais que chaque étudiant/profésseur est son propre couple d'identifiant. Cependant même ci cette technique pouvais être necessaire pour protéger l'api, la notre n'étant pas exposer à l'extérieur autrement que par l'interface web, cette solution est devenue inadapter et beaucoup trops complexe.

L'interface en elle même, afin de rendre l'experience utilisateur la plus simple et agréable possible, l'interface web à été principallement développé pour fonctionner sur mobile. Cette interface ce compose alors de quatres onglets.
Le premier onglet contiendra est une vue "dashboard", qui est un résumé de la salles actuellements séléctionné, on y trouvera par exemple le status des actifs pour savoir si ils sont en lignes ou pas.
Le second "application de la configuration" est dédié à l'application de tologie. C'est sur cette page que l'on pourra choisir la topologie que l'on souhaite déployer ainsi que de visualiser qu'elle topologie est actuellent en production. On pourra donc en sélèctionnant la classe, le groupe et le tp choisir la configuration adapté est la mettre en production.
Le troixieme onglet "création de configuration" a lui pour but de crée les différentes configurations. Pour cela, on est ammener à sélécionner les différents **vlans**, **trunk** et **interfaces** que l'on peut alors configurer manuellement avant de sauvegarder cette configuration pour la déployer ultérieurement.
Le dernier onglet "configuration On The Go" à pour fonction d'activer et désactiver les différentes interfaces avec un cliques.

Nous alons maintenant voir le but et fonctionnement du gestionnaire de topologie.
