+++
title = "BloodHound"
[menu.main]
  parent = "offsec"
  name = "BloodHound"
  weight = 20
+++





# Collector on the machine using SharpHound.exe
https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors



```
.\SharpHound.exe -c all -d active.htb -SearchForest
.\SharpHound.exe --EncryptZip --ZipFilename export.zip
.\SharpHound.exe -c all,GPOLocalGroup
.\SharpHound.exe -c all --LdapUsername <UserName> --LdapPassword <Password> --JSONFolder <PathToFile>
.\SharpHound.exe -c all -d active.htb --LdapUsername <UserName> --LdapPassword <Password> --domaincontroller 10.10.10.100
.\SharpHound.exe -c all,GPOLocalGroup --outputdirectory C:\Windows\Temp --randomizefilenames --prettyjson --nosavecache --encryptzip --collectallproperties --throttle 10000 --jitter 23
.\SharpHound.exe -c all,GPOLocalGroup --searchforest
```

# Collector on the machine using Powershell
https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1

```
Invoke-BloodHound -SearchForest -CSVFolder C:\Users\Public
Invoke-BloodHound -CollectionMethod All  -LDAPUser <UserName> -LDAPPass <Password> -OutputDirectory <PathToFile>
```


## Remotely via BloodHound Python
https://github.com/fox-it/BloodHound.py
```
pip install bloodhound
bloodhound-python -d lab.local -u rsmith -p Winter2017 -gc LAB2008DC01.lab.local -c all

```


# Neo4j Query
https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/

Visit URL once Neo4j is started

http://127.0.0.1:7474/browser/

Find All Users with an SPN/Find all Kerberoastable Users 
``` sql
MATCH (n:User)WHERE n.hasspn=true
RETURN n
```


Find SPNs with keywords (swap SQL with whatever)      

``` sql
MATCH (u:User) WHERE ANY (x IN u.serviceprincipalnames WHERE toUpper(x) CONTAINS 'SQL')RETURN u
```


Find what groups can reset passwords  
``` sql
MATCH p=(m:Group)-[r:ForceChangePassword]->(n:User) RETURN m.name, n.name ORDER BY m.name
```

Find what users have local admin rights              
``` SQL
MATCH p=(m:User)-[r:AdminTo]->(n:Computer) RETURN m.name, n.name ORDER BY m.name
```
