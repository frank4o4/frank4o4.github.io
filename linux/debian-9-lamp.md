
# Debian LAMP

I finally made the switch from Centos to Debian which I felt has more updated packages and much larger community.

Here are the steps I took to setup one of my web servers.



## MariaDB(MySQL)

To install MaridaDB on Stretch, just use apt to install the packages.


```
apt-get update
apt install mariadb-client mariadb-server
```

After Installation is complete run the following command to secure Mariadb


```
mysql_secure_installation
```

## Apache 2

To install Apache run the following command

```
apt-get install apache2
```


To run virtual host in a custom directory you will need to edit httpd.conf add the following lines



Let says your going to create a user called www and you want to run all your virtual host inside that directory. You will need to add the following to allow apache to serve the web files

```
<Directory /home/username/www/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
</Directory>
```

## PHP



To install PHP run the following command


```
apt install php php-mysql php-pear php-xml
```

Now Enable MariaDB and Apache to start up when the system boots up.


```
systemctl enable apache2
systemctl enable mysql
```

Lets starts up the services

```
systemctl start apache2
systemctl start mysql
```


Now lets test it works

Create a file called test.php

Copy code and paste code

``` php
<?php
echo phpinfo();
?>
```


Save and hit your IP address for example http://<yourIP>/test.php



You should see all the PHP module you have installed
