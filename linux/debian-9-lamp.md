---
layout: post
title: Debian 9 LAMP
date: 2018-04-12 14:09
author: frank
comments: true
categories: [Linux]
---
I finally made the switch from Centos to Debian which I felt has more updated packages and much larger community.

Here are the steps I took to setup one of my web servers.

&nbsp;

MariaDB(MySQL)

To install MaridaDB on Stretch, just use apt to install the packages.

&nbsp;

<code>apt-get update</code>

<code>apt install mariadb-client mariadb-server</code>

&nbsp;

After Installation is complete run the following command to secure Mariadb

&nbsp;

mysql_secure_installation

&nbsp;

&nbsp;

Apache 2

To install Apache run the following command

<code>apt-get install apache2</code>

&nbsp;

To run virtual host in a custom directory you will need to edit httpd.conf add the following lines

&nbsp;

Let says your going to create a user called www and you want to run all your virtual host inside that directory. You will need to add the following to allow apache to serve the web files

<code>
&lt;Directory /home/www/&gt;
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
&lt;/Directory&gt;
</code>

&nbsp;

PHP 7

&nbsp;

To install PHP 7 run the following command

&nbsp;

<code>apt install php7.0 php7.0-mysql php7.0-pear php7.0-xml</code>

&nbsp;

&nbsp;

Now Enable MariaDB and Apache to start up when the system boots up.

&nbsp;

<code>systemctl enable apache2</code>

<code>systemctl enable mysql</code>

Lets starts up the services

<code>systemctl start apache2</code>

<code>systemctl start mysql</code>

&nbsp;

Now lets test it works

Create a file called test.php

Copy code and paste code

<code>
&lt;?php</code><code>
echo phpinfo();</code><code>
?&gt;
</code>
Save and hit your IP address for example http://192.168.1.2/test.php

&nbsp;

You should see all the PHP module you have installed
