---
layout: post
title: NMAP
date: 2021-06-29 13:52
author: frank
comments: true
categories: [OSCP]
---
&nbsp;

<b>NMAP</b>

&nbsp;

Scan all ports and output to file

nmap -p- -sC -sV -o nmap.out  &lt;IP Address&gt;

&nbsp;

&nbsp;

TCP Scan all ports

sudo nmap -sC -sS -p0-65535 &lt;IP Address&gt;

&nbsp;

UDP Scanning top 20 ports

nmap -sU --top-ports 20 &lt;IP Address&gt;

UDP

Sudo nmap -sS -sU &lt;IP Address&gt;

&nbsp;

Quick Scan

nmap -sT -p- --min-rate 5000 &lt;IP Address&gt;

&nbsp;

&nbsp;

UDP Scan

sudo nmap --top-ports 100 -sU -o udp.scan

&nbsp;
