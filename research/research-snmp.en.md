---
title: "Research SNMP"
date: 2021-10-20T17:03:39Z
tags: ["research","snmp"]
draft: false
---
This files is composed of all the test done during the primary research for the SDN CloudStack project.

## MIBs (Management Information Base) used

- CISCO-VLAN-IFTABLE-RELATIONSHIP-MIB.my
- CISCO-VLAN-MEMBERSHIP-MIB.my
- CISCO-VTP-MIB.my

All those MIBs can be found from the maker FTP in accordance with the following notice : https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750/software/release/12-2_44_se/configuration/guide/scg/swmibs.pdf

## Raw data

The raw data where stored inside .txt files, under the CSV format.
 
## Formatted data

The data are then shaped with Excel.

The formul to get the final ID is = `RIGHT(A3,LEN(A3) - SEARCH(".",A3))`(can be modified as needed)

## Data summary 

At this time, the data we got are :

| Raw files name | Formed files name | Description |
|---------------------|-----|------|
| walk_rtstack.txt | walk_rtstack.xlsx | General Walk realised on the RTSTACK switch|
| walk_rtstack2.txt | walk_rtstack2.xlsx | Second general walk realised on the RTSTACK switch. Contains more data|
| vlanmembership_rtstack.txt | vlanmembership_rtstack.xlsx | Subtree of the MIB CISCO-VLAN-MEMBERSHIP-MIB from "ciscoVlanMembershipMIBObjects" |
| vtpvlantable_rtstack.txt | vtpvlantable_rtstack.xlsx | Subtree of the  MIB CISCO-VTP-MIB from "vlanInfo" |
| iface-vlan_rtstack.txt | iface-vlan_rtstack.txt | Relation beetween the interface-vlan and the RTSTACK, more information below... |

## Interface-vlan

Path MIB : `1 (iso). 3 (org). 6 (dod). 1 (internet). 4 (private). 1 (enterprises). 9 (cisco). 9 (ciscoMgmt). 68 (ciscoVlanMembershipMIB). 1 (ciscoVlanMembershipMIBObjects). 2 (vmMembership). 2 (vmMembershipTable). 1 (vmMembershipEntry). 2 (vmVlan)`
OID : `1.3.6.1.4.1.9.9.68.1.2.2.1.2`

That send back the relation VLAN-INTERFACE to the Switch.

## Trunks

To retrieve and manage trunks, we use the CISCO-VTP-MIB. \
In this MIB, we use the vlanTrunkPortTable, which lists all the information we need, namely
- Interface index
- Authorized or "tagged" vlans
- Native Vlan
- Status of the interface "trunking"/"not trunking

The tagged VLANS are represented by a string byte, of the form : \
Name/OID: vlanTrunkPortVlansEnabled.10535 ; Value (StringOctet): 0x00 00 00 00 00 00 00 00 88 80 80 20 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 70 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00`

Once transformed into binary, this value allows to recover the "authorized on the trunk" status of each VLAN, thanks to the status of the corresponding bit. \
Example : Bit 80 represents the state of VLAN 80, if it is set to '1', the vlan is authorized on the trunk.

These OIDs are read/write, which means that a different configuration can be pushed on these OIDs. So you just have to change the state of a bit, rebuild the string byte, then push it with snmpset to allow or block a vlan on the trunk.
