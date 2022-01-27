---
title: "List des URL de L'API"
date: 2021-10-17T12:42:10Z
tags: ["notice","api"]
draft: false
---

Liste des foction requise pour l'API et les URL corespondante.
## GET

### Section générale
|Action                    	 		| URL                   			|
|:----------------------------------------------|:----------------------------------------------|
|obtenir la configuration global actuelle	| /api/v1/running-config			|
	

### Section des Vlan
|Action                     			| URL                  				|
|:----------------------------------------------|:----------------------------------------------|
|obtenir la liste de tous les vlan		| /api/v1/vlan/all 				|
|obtenir les info d'un vlan spécifique par id	| /api/v1/vlan/{vlan_id}			|
|obtenir les info d'un vlan spécifique par nom	| /api/v1/vlan/{vlan_name}			|
|obtenir les interfaces membre d'un vlan par id	| /api/v1/vlan/{vlan_id}/interface		|
|obtenir les interfaces membre d'un vlan par nom| /api/v1/vlan/{vlan_name}/interface		|


### Section des Interface
|Action                     			| URL                   			|
|:----------------------------------------------|:----------------------------------------------|
|obtenir la liste de toutes les interfaces	| /api/v1/interface/all				|
|obtenir les interfaces voisine d'une interface	| /api/v1/interface/{interface_id}/neighbor	|
|obtenir les info d'une interface spécifique	| /api/v1/interface/{interface_id}		|
|obtenir les @IP de toutes les interfaces	| /api/v1/interface/all/ip			|
|obtenir l'@IP d'une interface spécifique	| /api/v1/interface/{interface_id}/ip		|
|obtenir le status de toutes les interfaces	| /api/v1/interface/all/status			|
|obtenir le status d'une interface spécifique	| /api/v1/interface/{interface_id}/status	|


### Section des Switchs
|Action						|						|
|:----------------------------------------------|:----------------------------------------------|
|obtenir les propriétées d'un switch		| /api/v1/switch/{switch_id}			|
|obtenir la liste des vlans d'un switch		| /api/v1/switch/{switch_id}/vlan		|
## SET

### Section générale
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|définir une nouvelle configuration global	| /api/v1/running-config/{config_id} 		|

### Vlan Section
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|						|						|

### Interface Section
|Action								| URL						|
|:--------------------------------------------------------------|:----------------------------------------------|
|définir un nouveau mode d'acces à toutes les interfaces	| /api/v1/interface/all/{mode}			|
|définir un nouveau mode d'acces à une interface spécifique 	| /api/v1/interface/{interface_id}/{mode}	|
|définir un même vlan à toutes les interfaces			| /api/v1/interface/all/{vlan_id}		|
|définir un vlan à une interface spécifique			| /api/v1/interface/{interface_id}/{vlan_id}	|

