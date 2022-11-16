---
layout: post
title: Upgrading Nexus 9508 NX OS
date: 2018-03-20 14:36
author: frank
comments: true
categories: [Network]
---
<ol>
 	<li>
<div><span style="color: #1f497d;">Backup the running config off of the switch
</span></div></li>
 	<li>
<div><span style="color: #1f497d;">Verify you have sufficient space on both Sup's; delete older unused file images (not the current image!) if required
</span></div>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">dir bootflash://sup-local/
</span></p>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">dir bootflash://sup-standby/
</span></p>
</li>
</ol>
<ol>
 	<li>
<div><span style="color: #1f497d;">Copy the image to the active Sup.  I find FTP the easiest
</span></div>
<p style="margin-left: 36pt;"><span style="color: #1f497d; font-family: Lucida Console;">     <span style="color: red;">copy <a><span style="color: blue; text-decoration: underline;">ftp://user@&lt;ftp-IP&gt;/nxos.7.0.3.I2.2d.bin</span></a> bootflash: nxos.7.0.3.I2.2d.bin
</span></span></p>
</li>
 	<li>
<div><span style="color: #1f497d;">Verify checksum
</span></div>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">show file bootflash://sup-1/nxos.7.0.3.I2.2d.bin sha256sum
</span></p>
<span style="color: #1f497d;">                Result should be:
</span>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">d02606aba9f95563d1be810f4b5c0795db5c87ee50f5e552dc4de9015264d18b4ab69e3ad51558e19e04046d3c4319c8378b0ad6d493b8cdcb25a12d7c6806f4
</span></p>
</li>
 	<li>
<div><span style="color: #1f497d;">Verify install impact
</span></div>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">show install all impact nxos bootflash:nxos.7.0.3.I2.2d.bin
</span></p>
</li>
 	<li>
<div><span style="color: #1f497d;">Save the running config
</span></div>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">copy running-config startup-config
</span></p>
</li>
 	<li>
<div><span style="color: #1f497d;">Launch the install script.  For the current version it will be impactful (forced reload)
</span></div>
<p style="margin-left: 36pt;"><span style="color: red; font-family: Lucida Console;">install all nxos bootflash:nxos.7.0.3.I2.2d.bin
</span></p>
</li>
</ol>
