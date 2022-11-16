---
layout: post
title: NSLOOKUP DNS tool
date: 2018-03-20 17:08
author: frank
comments: true
categories: [Linux, Windows]
---
I find nslookup a very good tool when trouble shooting DNS records, here are some examples on how it can be used.

&nbsp;

Note you can use this on Linux,Windows and MAC.

If you opened up your command prompt and type in nslookup.

first let tell nslookup which dns server to query

server 8.8.8.8

in my example I'm using google public dns server

let says you want to find the IP address of example.org

you would just type in

example.org

<img class="alignnone size-full wp-image-71" src="http://frankmancuso.ca/wp-content/uploads/2018/03/nslookup1.jpg" alt="" width="226" height="173" />

&nbsp;

Now lets say you want to see what dns server example.org uses

&nbsp;

type in

set type=ns

Now type in example.org

<img class="alignnone size-full wp-image-72" src="http://frankmancuso.ca/wp-content/uploads/2018/03/nslookup2.jpg" alt="" width="414" height="174" />

&nbsp;

Let check what mail server gmail.com uses ( example.org didnt have any records so I decided to use gmail)

type in

&nbsp;

set type=mx

now type in gmail.com

<img class="alignnone size-full wp-image-73" src="http://frankmancuso.ca/wp-content/uploads/2018/03/nslookup3.jpg" alt="" width="552" height="246" />

&nbsp;

Let also check what spam filter gmail uses

type in

set type=txt

type in now gmail.com

&nbsp;

<img class="alignnone size-full wp-image-74" src="http://frankmancuso.ca/wp-content/uploads/2018/03/nslookup4.jpg" alt="" width="455" height="157" />

&nbsp;

Other type of records you would most commonly look at are A and CNAME

set type=CNAME

set type=A

&nbsp;

&nbsp;
