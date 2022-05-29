---
title: "Recherche SNMP"
date: 2021-10-20T17:03:39Z
tags: ["research","snmp"]
draft: false
---

Cette page contient les tests effectués durant les recherches préparatoires pour le projet SDN CloudStack.

## MIBs utilisées

- CISCO-VLAN-IFTABLE-RELATIONSHIP-MIB.my
- CISCO-VLAN-MEMBERSHIP-MIB.my
- CISCO-VTP-MIB.my

Toutes ces MIBs sont récuperables sur le FTP du constructeur conformément à cette fiche : https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750/software/release/12-2_44_se/configuration/guide/scg/swmibs.pdf

## Résultats bruts

Les résultats bruts sont stockés dans des fichiers .txt, sous forme de CSV.

## Résultats mis en forme 

Les résultats sont ensuite mis en forme avec Excel.

La formule pour récupérer l'ID final est : `=DROITE(A2;NBCAR(A2) - CHERCHE(".";A2))`(a modifier au besoin)

## Réapitulatif des résultats

A l'heure actuelle, les résultats présents sont :

| Nom du fichier brut | Nom du fichier mis en forme | Description |
|---------------------|-----|------|
| walk_rtstack.txt | walk_rtstack.xlsx | Walk général effectué sur le switch RTSTACK |
| walk_rtstack2.txt | walk_rtstack2.xlsx | Second walk général effectué sur le switch RTSTACK. Contient plus d'informations |
| vlanmembership_rtstack.txt | vlanmembership_rtstack.xlsx | Subtree de la MIB CISCO-VLAN-MEMBERSHIP-MIB à partir de "ciscoVlanMembershipMIBObjects" |
| vtpvlantable_rtstack.txt | vtpvlantable_rtstack.xlsx | Subtree de la MIB CISCO-VTP-MIB à partir de "vlanInfo" |
| iface-vlan_rtstack.txt | iface-vlan_rtstack.txt | Correspondance interface-vlan de la RTSTACK, plus d'infos ci-dessous... |

## Interface-vlan

Chemin MIB : `1 (iso). 3 (org). 6 (dod). 1 (internet). 4 (private). 1 (enterprises). 9 (cisco). 9 (ciscoMgmt). 68 (ciscoVlanMembershipMIB). 1 (ciscoVlanMembershipMIBObjects). 2 (vmMembership). 2 (vmMembershipTable). 1 (vmMembershipEntry). 2 (vmVlan)`
OID : `1.3.6.1.4.1.9.9.68.1.2.2.1.2`

Ceci renvoie la correspondance VLAN-INTERFACE sur le Switch.

## Trunks

Pour récupérer et gérer les trunks, on utilise la CISCO-VTP-MIB. \
Dans cette MIB, on utilise la table vlanTrunkPortTable, qui recense toutes les informations dont nous avons besoin, à savoir :
- Index de l'interface
- Vlans autorisés ou "taggés"
- Vlan natif
- Statut de l'interface "trunking"/"not trunking"

Les VLANS taggés sont représentés par un octet string, de la forme : \
`Name/OID: vlanTrunkPortVlansEnabled.10535; Value (OctetString): 0x00 00 00 00 00 00 00 00 88 80 80 20 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 70 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00`

Une fois transformé en binaire, cette valeur permet de récupérer l'état "autorisé sur le trunk" de chaque VLAN, grâce à l'état du bit correspondant. \
Exemple : Le bit 80 représente l'état du VLAN 80, s'il est à '1', le vlan est autorisé sur le trunk.

Ces OIDs sont en read/write, ce qui signifie qu'on peut pousser une configuration différente sur ces OIDs. Il suffit donc de changer l'état d'un bit, de reconstruire l'octet string, puis de le pousser avec snmpset pour autoriser ou bloquer un vlan sur le trunk.

