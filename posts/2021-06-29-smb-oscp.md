---
layout: post
title: SMB OSCP
date: 2021-06-29 13:48
author: frank
comments: true
categories: [OSCP]
---
<div style="direction: ltr; border-width: 100%;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 12.6243in;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 12.6243in;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Use Nmap to Scan host for smb exploits</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">sudo nmap --scripts=smb-vul* &lt;IP Address&gt;</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">sudo nmap --script=smb-enum* &lt;IP Address&gt;</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">nmap -v -p 139, 445 --script=smb-os-discovery 10.11.1.227</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>

<div style="direction: ltr;">
<table style="direction: ltr; border-collapse: collapse; border: 0pt solid #A3A3A3;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: .993in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;"><span style="font-weight: bold;">SMB Version</span></p>
</td>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: 4.8645in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;"><span style="font-weight: bold;">Windows version</span></p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">CIFS</p>
</td>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Microsoft Windows NT 4.0</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 1.0</p>
</td>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: 4.9534in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows 2000, Windows XP, Windows Server 2003 and Windows Server 2003 R2</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 2.0</p>
</td>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows Vista &amp; Windows Server 2008</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 2.1</p>
</td>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows 7 and Windows Server 2008 R2</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 3.0</p>
</td>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows 8 and Windows Server 2012</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 3.0.2</p>
</td>
<td style="border-width: 0pt; background-color: white; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows 8.1 and Windows Server 2012 R2</p>
</td>
</tr>
<tr>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: .9736in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">SMB 3.1.1</p>
</td>
<td style="border-width: 0pt; background-color: #eeeeee; vertical-align: top; width: 4.884in; padding: 2.0pt 3.0pt 2.0pt 3.0pt;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 10.5pt; color: black;">Windows 10 and Windows Server 2016</p>
</td>
</tr>
</tbody>
</table>
</div>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 9.0pt; color: #595959;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">To be able to download all files on a smb share.</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">smbclient '<a href="file://server/share">\\server\share</a>'
mask ""
recurse ON
prompt OFF
cd 'path\to\remote\dir'
mget *</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Rpcclient is a good tool for enumerating smb</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;"># The -U is used for null username</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">Rpcclient -U '' 10.11.1.17</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">rpcclient $&gt; querydomainfo</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">command not found: querydomainfo</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">rpcclient $&gt; querydominfo</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Domain:                WORKGROUP</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Server:                LUCKY</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Comment:        lucky server (Samba, Ubuntu)</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Total Users:        0</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Total Groups:        0</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Total Aliases:        0</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Sequence No:        1608749220</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Force Logoff:        -1</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Domain Server State:        0x1</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Server Role:        ROLE_DOMAIN_PDC</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">Unknown 3:        0x1</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"># Used to retrieve list of users present on the system</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">rpcclient $&gt; enumdomusers</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"># Used to query user info</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;">rpcclient $&gt; queryuser [username]</p>
<p lang="en-US" style="margin: 0in; margin-left: .75in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; margin-left: .375in;"><img src="file:///C:/Users/T03401/AppData/Local/Temp/msohtmlclip1/02/clip_image001.png" alt="rpcclient $&gt; enum 
enumalsgroups 
enumtrust 
enumdata 
enumdataex 
enumdomains 
enumdomgroups 
enumdomusers 
enumdrivers 
enumforms 
enumjobs 
enumkey 
enummonitors 
enumports 
enumprinters 
enumprivs 
enumprocdatatypes 
enumprocs " width="1557" height="257" />

<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Scan netbios information on host</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">sudo nbtscan -r &lt;IP ADDRESS&gt;</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">enum4linux - SMB shares can be enumerated via enum4linux.</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">enum4linux [IP]</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">List SMB shares on host</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">smbmap -H 10.10.10.100</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Start Simple smb share using python</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">python3 /usr/share/doc/python3-impacket/examples/smbserver.py tools .</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">Python2 /usr/share/doc/python3-impacket/examples/smbserver.py tools .</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">python smbserver.py share /home/kali/FTP</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Samba Client connection from Linux</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">smbclient -L \\\\10.10.10.4\\</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">smbclient //10.10.10.100/Replication</p>

</div>
</div>
</div>
