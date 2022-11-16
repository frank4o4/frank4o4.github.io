---
layout: post
title: Install Pfsense
date: 2018-03-20 19:39
author: frank
comments: true
categories: [Secruity]
---
I thought it would be a good time to dig deep and see what is really going on in my network at home with all these smart devices you don't know what they are doing until you use something like wireshark or a firewall which you can deep dive into the packets this is why I chose to go with Pfsense and snort.

&nbsp;

To start off visit

http://www.pfsense.org

download ISO installation media. Once your done burning CD boot off media

Select The Install and enter for OK

<img class="alignnone size-full wp-image-136" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense1.jpg" alt="" width="724" height="400" />

Select your keyboard layout, in my case I left it the default and hit enter

<img class="alignnone size-full wp-image-137" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense2.jpg" alt="" width="719" height="388" />

Leave the Auto (UFS) which is default and click OK

&nbsp;

<img class="alignnone size-full wp-image-139" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense3.jpg" alt="" width="718" height="402" />

Now pfsense will begin to install

&nbsp;

<img class="alignnone size-full wp-image-140" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense4.jpg" alt="" width="723" height="402" />

Now installation is complete select No cause we will do everything via HTTP later Now hit Enter on next screen to reboot.

<img class="alignnone size-full wp-image-141" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense5.jpg" alt="" width="721" height="397" />

&nbsp;

Once system boots up we need to setup our LAN IP so we can access the web broswer.

Select option 1

&nbsp;

<img class="alignnone size-full wp-image-142" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense6.jpg" alt="" width="671" height="427" />

Now you will be asked if your going to run any network adapters as a trunk port to a switch. In this example we won't do that so select N for no

<img class="alignnone size-full wp-image-143" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense7.jpg" alt="" width="753" height="180" />

&nbsp;

Select your WAN interface in my case it is em0

<img class="alignnone size-full wp-image-145" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense8.jpg" alt="" width="599" height="100" />

Now select your LAN interface in my case it is em1

<img class="alignnone size-full wp-image-146" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense9.jpg" alt="" width="513" height="61" />

&nbsp;

After you will be asked to verify the changes. Select y for yes

<img class="alignnone size-full wp-image-147" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense10.jpg" alt="" width="452" height="133" />

Once complete we will not setup our LAN interface IP Address

Select option 2

<img class="alignnone size-full wp-image-142" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense6.jpg" alt="" width="671" height="427" />

&nbsp;

Now Select adapter LAN in this example it is number 2

<img class="alignnone size-full wp-image-150" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense11.jpg" alt="" width="597" height="143" />

&nbsp;

In my example I will setup IP address 192.168.1.1 with the submask of 255.255.255.0

<img class="alignnone size-full wp-image-151" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense12.jpg" alt="" width="588" height="93" />

&nbsp;

Hit enter we will not setup a default gateway because our ISP is our gateway to the internet

<img class="alignnone size-full wp-image-152" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense13.jpg" alt="" width="626" height="74" />

Hit Enter no IPV6 gateway

<img class="alignnone size-full wp-image-154" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense14-1.jpg" alt="" width="523" height="50" />

&nbsp;

If you want to setup pfsense to run DHCP select Y other wise select N

<img class="alignnone size-full wp-image-155" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense15.jpg" alt="" width="519" height="35" />

Select Yes to allow LAN users to access the HTTP URL

<img class="alignnone size-full wp-image-156" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense16.jpg" alt="" width="683" height="33" />

Now you should see you can access your pfsense box by http://192.168.1.1

<img class="alignnone size-full wp-image-157" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense17.jpg" alt="" width="817" height="123" />

Now login to your pfsense firewall with

username = admin

password = pfsense

<img class="alignnone size-full wp-image-158" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense18.jpg" alt="" width="1333" height="655" />

Once you login you will want to setup your WAN interface, if your using cable internet then most cases it should be configured.

<img class="alignnone size-full wp-image-159" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense19.jpg" alt="" width="1179" height="414" />

Select Interface from the menu and select WAN

<img class="alignnone size-full wp-image-160" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense20.jpg" alt="" width="547" height="230" />

&nbsp;

If your using DSL you will need to put your modem in bridge mode. In my case I had to login to my provider modem and change the dsl username and password so the router would fail to login and then configure my pfsense PPPoe with the username and password.

&nbsp;

Now your complete see my other posts showing you how to configure snort and port forwarding.

<img class="alignnone size-full wp-image-161" src="http://frankmancuso.ca/wp-content/uploads/2018/03/pfsense21.jpg" alt="" width="1140" height="674" />
