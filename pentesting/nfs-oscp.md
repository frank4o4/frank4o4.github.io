---
layout: post
title: NFS OSCP
date: 2021-06-29 13:54
author: frank
comments: true
categories: [OSCP]
---
<div style="direction: ltr; border-width: 100%;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 3.9993in;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 3.9993in;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">NMAP Script</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">nmap -sV -p 111 --script=rpcinfo 10.11.1.1-254</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">nmap -p 111 --script nfs* 10.11.1.72</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Mount NFS</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">mkdir john</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">Sudo mount -o nolock 10.1.1.72:/home/john john</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Showmount to show nfs shares</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">Showmount -e [IP]</p>

</div>
</div>
</div>
