---
title: "Api Url List"
date: 2021-10-17T12:42:10Z
tags: ["notice","api"]
draft: false
---

Liste of fonction needed for the API and the corresponding URL.

## GET

### General Section
|Action                    	 		| URL                   			|
|:----------------------------------------------|:----------------------------------------------|
|get running config		 		| /api/v1/running-config			|
	

### Vlan Section
|Action                     			| URL                  				|
|:----------------------------------------------|:----------------------------------------------|
|get all vlan list      			| /api/v1/vlan/all 				|
|get specific vlan info by id 			| /api/v1/vlan/{vlan_id}			|
|get specific vlan info by name			|  /api/v1/vlan/{vlan_name}			|
|get specific vlan interface member by id 	| /api/v1/vlan/{vlan_id}/interface		|
|get specific vlan interface member by name 	| /api/v1/vlan/{vlan_name}/interface		|


### Interface Section
|Action                     			| URL                   			|
|:----------------------------------------------|:----------------------------------------------|
|get all interface list 			| /api/v1/interface/all				|
|get inerface neighbor  			| /api/v1/interface/neighbor			|
|get specific interface info by id  		| /api/v1/interface/{interface_id}		|
|get all interface @IP				| /api/v1/interface/all/ip			|
|get specific interface @IP			| /api/v1/interface/{interface_id}/ip		|
|get all interface status			| /api/v1/interface/all/status			|
|get specific interface status			| /api/v1/interface/{interface_id}/status

### Switch Section
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|get specific switch property			| /api/v1/switch/{switch_id}			|
|get the vlan list of a specific switch		| /api/v1/switch/{switch_id}/vlan		|



## SET

### General Section
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|set new running config				| /api/v1/running-config/{config_id} 		|

### Vlan Section
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|						|						|

### Interface Section
|Action						| URL						|
|:----------------------------------------------|:----------------------------------------------|
|set all interface mode				| /api/v1/interface/all/{mode}			|
|set specific interface mode			| /api/v1/interface/{interface_id}/{mode}	|
|set all interface to vlan			| /api/v1/interface/all/{vlan_id}		|
|set specific interface to vlan			| /api/v1/interface/{interface_id}/{vlan_id}	|

