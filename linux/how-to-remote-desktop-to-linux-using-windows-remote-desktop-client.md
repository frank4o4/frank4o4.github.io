---
layout: post
title: How to Remote Desktop to Linux using Windows Remote Desktop client
date: 2019-03-28 18:25
author: frank
comments: true
categories: [Linux]
---
<!-- wp:paragraph -->
<p>If you would like to be able to use your Windows Remote Desktop client to remote desktop to your Linux desktop you have come in the right place.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This will work on most Debian based Linux, I've tested on Ubuntu. MX Linux and Debian.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>First you will need to launch your Shell terminal or use putty to ssh to the Linux server.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>apt-get install xrdp</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code>apt-get install tigervnc-standalone-server</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code" lang="c" escaped="true"><code>cd /etc/xrdp/

cat &lt;</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code>MX Linux
service xrdp restart

Debian
systemctl restart xrdp

If you want XRDP to start up when the system starts up use this command

systemctl enable xrdp</code></pre>
<!-- /wp:code -->
<p>&nbsp;</p>
<!-- wp:paragraph -->
<p><br />Now launch your Windows Remote Desktop client and you should be able to RDP to your Linux box.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->
