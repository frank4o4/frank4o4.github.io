---
layout: post
title: Centos 7 x64 Elastic Search 6.2
date: 2018-04-12 14:13
author: frank
comments: true
categories: [Linux]
---
In my development environment I have been playing around with Elastic search and have to say it is pretty neat how you can centralize your windows logs and view them on Kibanna.

&nbsp;

If you want to install here are the steps I took.

&nbsp;

I installed Centos 7 x64 with the minimum installation

After install I installed the following tools

&nbsp;

You will need wget and if you want tools like ifconfig and nano editor.

<code>
yum install nettools nano wget curl
</code>
We need Java 8 so using yum

<code>
yum install java-1.8.0-openjdk.x86_64
</code>

&nbsp;

Now we need to download the public signing key from elastic

<code>
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
</code>

Using your favorite Linux editor

<code>
nano -w /etc/yum.repos.d/elastic.repo
</code>

Now paste the following

<code>
[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
</code>
hit Ctrl X to save

&nbsp;

Now lets install elasticsearch

<code>
yum install elasticsearch
</code>

Running elasticsearch with systemd

<code>
systemctl daemon-reload
</code>

<code>
systemctl enable elasticsearch.service
</code>

Before starting elasticsearch lets edit the configuration file

&nbsp;

<code>
nano -w  /etc/elasticsearch/elasticsearch.yml
</code>

&nbsp;

Find Line network.host and change it so the # in front is deleted and looks like this

<code>
network.host: 0.0.0.0
</code>

Hit Ctrl X to save

This would make elasticsearch listen on any IP address the server is running. In production you can use x-pack to secure the server so only hosts with the username and password can access the elasticsearch

&nbsp;

Now Lets start

elasticsearch

<code>
systemctl start elasticsearch.service
</code>

Now to verify the service is running you can query with curl

<code>
curl http://127.0.0.1:9200
</code>

You should get a similar output

<code>
{
"name" : "esnode-1",
"version" : {
"number" : "6.2.1",
"build_hash" : "7299dc3",
"build_date" : "2018-02-07T19:34:26.990113Z",
"build_snapshot" : false,
"lucene_version" : "7.2.1",
"minimum_wire_compatibility_version" : "5.6.0",
"minimum_index_compatibility_version" : "5.0.0"
},
"tagline" : "You Know, for Search"
}
</code>

&nbsp;

Now your complete
