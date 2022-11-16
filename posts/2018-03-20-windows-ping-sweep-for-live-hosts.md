---
layout: post
title: Windows Ping Sweep for live hosts
date: 2018-03-20 17:08
author: frank
comments: true
categories: [Windows]
---
I used this one day to see how many IP's I was using in the network by doing a ping sweep.

<strong>for /l %i in (1,1,254) do @ping 192.168.1.%i -n 1 -w 100 | find "Reply"</strong>

This will ping all addresses from 192.168.1.1 to 192.168.1.254 one time each, wait 100ms for a reply.

<strong>for /l %i in (1,1,254) do @ping 192.168.1.%i -n 1 -w 100 | find "timed out"</strong>

This would let you know what is not in use if you were looking for a free IP address.

If you want to pipe it to a text file use &gt;&gt; filename.txt at the end of the command.

&nbsp;

Now if you want to see if the IP has a DNS record for example if the host got a DHCP address most cases it would of sent it's hostname, use the following command with IP address

ping -a 192.168.1.1
