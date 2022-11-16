---
layout: post
title: Cisco NetFlow IOS And IOS XE
date: 2018-04-12 13:37
author: frank
comments: true
categories: [Network]
---
Cisco IOS Steps

Configure the following on the interface you want to capture netflows on. Most cases you would enable on WAN and LAN

<code>
interface gig0/0/0
description WAN
ip nbar protocol-discovery
ip flow ingress</code>
</code>

<code>
interface gig0/0/1
description LAN
ip nbar protocol-discovery
ip flow ingress
</code>

Now Configure your Flow Exporter

You will export to your netflow server via the LAN interface unless its cloud based.

<code>
ip flow-export source GigabitEthernet0/0/1
</code>
Change the IP address and the port destination

<code>
ip flow-export destination 192.168.1.5 9999
</code>


Cisco IOS XE is a lot different to configure NetFlow here are the steps

First let configure our netflow exporter
<code>
flow exporter netflow
destination 192.168.1.5
source GigabitEthernet0/0/1
transport udp 9999
export-protocol netflow-v5
</code>

Now Let configure the netflow Monitor

<code>
flow monitor netflow
exporter netflow
record netflow-original
</code>

Now configure your interfaces

<code>
Interface gig0/0/0
description WAN
ip flow monitor netflow input
ip nbar protocol-discovery
</code>

<code>
Interface gig0/0/1
description LAN
ip flow monitor netflow input
ip nbar protocol-discovery
</code>
