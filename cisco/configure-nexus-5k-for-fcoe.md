---
layout: post
title: Configure Nexus 5k for FCOE
date: 2018-03-02 21:22
author: frank
comments: true
categories: [Network]
---
This article is a quick glance on how to configure Nexus 5K for Fiber Channel over Ethernet
&nbsp;
Configure VLAN
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">Conf t
Vlan 1010
Fcoe vsan 10
Name Fabric_A</td>
</tr>
</tbody>
</table>
&nbsp;
Configure vsan database
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">Conf t
Vsan database
Vsan 10
vsan 10 interface fc1/35</td>
</tr>
</tbody>
</table>
&nbsp;
Configure virtual fiber channel
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">interface vfc11
 bind interface Ethernet1/11
 switchport trunk allowed vsan 10
 no shutdown</td>
</tr>
</tbody>
</table>
&nbsp;
Add vfc to vsan database
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">Conf t
Vsan database
Vsan 10 interface vfc 11</td>
</tr>
</tbody>
</table>
&nbsp;
Configure Ethernet interface to allow vsan vlan
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">interface Ethernet1/11
 description BRM-VM1
 switchport mode trunk
 switchport trunk native vlan 999
 switchport trunk allowed vlan 101-105,1010
 spanning-tree port type edge trunk</td>
</tr>
</tbody>
</table>
Configure Device Alias
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">BRM-5K-1-R3# show flogi database
--------------------------------------------------------------------------------
INTERFACE VSAN FCID PORT NAME NODE NAME
--------------------------------------------------------------------------------
fc1/41 10 0x3e0000 20:70:00:c0:ff:27:09:d7 20:80:00:c0:ff:27:09:d7
 [msa_ctl_A1]
fc1/42 10 0x3e0041 24:70:00:c0:ff:27:09:d7 20:80:00:c0:ff:27:09:d7
 [msa_ctl_B1]
vfc11 10 0x3e0060 10:00:b0:5a:da:02:93:b1 20:00:b0:5a:da:02:93:b1
 [vm1_P1]
vfc12 10 0x3e0080 10:00:b0:5a:da:02:63:11 20:00:b0:5a:da:02:63:11
 [vm2_P1]
vfc13 10 0x3e00a0 10:00:b0:5a:da:02:53:f1 20:00:b0:5a:da:02:53:f1
 [vm3_P1]
Total number of flogi = 5.
device-alias database
 device-alias name vm1_P1 pwwn 10:00:b0:5a:da:02:93:b1
 device-alias name vm2_P1 pwwn 10:00:b0:5a:da:02:63:11
 device-alias name vm3_P1 pwwn 10:00:b0:5a:da:02:53:f1
 device-alias name msa_ctl_A1 pwwn 20:70:00:c0:ff:27:09:d7
 device-alias name msa_ctl_B1 pwwn 24:70:00:c0:ff:27:09:d7
device-alias commit</td>
</tr>
</tbody>
</table>
Configure Zone
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">zone name vm1_to_msa vsan 10
 member pwwn 10:00:b0:5a:da:02:93:b1
! [vm1_P1]
 member pwwn 20:70:00:c0:ff:27:09:d7
! [msa_ctl_A1]
 member pwwn 24:70:00:c0:ff:27:09:d7
! [msa_ctl_B1]
zone name vm2_to_msa vsan 10
 member pwwn 10:00:b0:5a:da:02:63:11
! [vm2_P1]
 member pwwn 24:70:00:c0:ff:27:09:d7
! [msa_ctl_B1]
 member pwwn 20:70:00:c0:ff:27:09:d7
! [msa_ctl_A1]
zone name vm3_to_msa vsan 10
 member pwwn 10:00:b0:5a:da:02:53:f1
! [vm3_P1]
 member pwwn 24:70:00:c0:ff:27:09:d7
! [msa_ctl_B1]
 member pwwn 20:70:00:c0:ff:27:09:d7
! [msa_c</td>
</tr>
</tbody>
</table>
&nbsp;
Configure Zoneset
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">zoneset name Fabric_A vsan 10
 member vm1_to_msa
 member vm2_to_msa
 member vm3_to_msa</td>
</tr>
</tbody>
</table>
&nbsp;
Activate Zone
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 623px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="padding-left: 7px; padding-right: 7px; border: solid 0.5pt;">zoneset activate name Fabric_A vsan 10</td>
</tr>
</tbody>
</table>
