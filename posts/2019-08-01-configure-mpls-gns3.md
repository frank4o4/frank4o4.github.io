---
layout: post
title: Configure MPLS GNS3
date: 2019-08-01 18:44
author: frank
comments: true
categories: [Network]
---
In this article you can use it to see how a MPLS works in production on a small scale. In production you would have much more Routers to configure but this will get you started in your journey of learning MPLS.

&nbsp;

Requirements

GNS3 with Router IMAGE

<img class="alignnone wp-image-293" src="http://frankmancuso.ca/wp-content/uploads/2019/08/mpls-1-300x117.jpg" alt="" width="328" height="128" />

First start off by connecting your Routers as follows

PE1 to BB1 and PE2 to BB1, you can name your routers anything you want.

&nbsp;

Now lets configure a IP topology so they can talk

&nbsp;

PE1

conf t

interface Loopback0
ip address 2.2.2.2 255.255.255.255
ip ospf 1 area 0
!

interface FastEthernet0/0
ip address 10.0.1.2 255.255.255.0
ip ospf 1 area 0
no shutdown

BB1

interface Loopback0
ip address 1.1.1.1 255.255.255.255
ip ospf 1 area 0

interface FastEthernet0/0
ip address 10.0.1.1 255.255.255.0
ip ospf 1 area 0

interface FastEthernet1/0
ip address 10.0.2.1 255.255.255.0
ip ospf 1 area 0

&nbsp;

PE2

interface Loopback0
ip address 3.3.3.3 255.255.255.255
ip ospf 1 area 0

interface FastEthernet1/0
ip address 10.0.2.2 255.255.255.0
ip ospf 1 area 0

&nbsp;

Now you should slowly see your Routers establish OSPF

PE1

%OSPF-5-ADJCHG: Process 1, Nbr 1.1.1.1 on FastEthernet0/0 from LOADING to FULL, Loading Done

&nbsp;

Lets Configure BGP Sesson between PE1 and PE2

&nbsp;

PE1

&nbsp;

router bgp 65001
bgp log-neighbor-changes
neighbor 3.3.3.3 remote-as 65001
neighbor 3.3.3.3 update-source Loopback0

address-family vpnv4
neighbor 3.3.3.3 activate
neighbor 3.3.3.3 send-community extended
exit-address-family

&nbsp;

&nbsp;

PE2

&nbsp;

router bgp 65001
bgp log-neighbor-changes
neighbor 2.2.2.2 remote-as 65001
neighbor 2.2.2.2 update-source Loopback0
!
address-family vpnv4
neighbor 2.2.2.2 activate
neighbor 2.2.2.2 send-community extended
exit-address-family

BGP Neighbor established output on PE2

PE2

%BGP-5-ADJCHANGE: neighbor 2.2.2.2 Up

&nbsp;

Lets turn on MPLS with LDP

PE1

conf t

mpls label protocol ldp

router ospf 1
mpls ldp sync

interface FastEthernet0/0
ip mpls

PE2

conf t

mpls label protocol ldp

router ospf 1
mpls ldp sync

interface FastEthernet1/0
ip mpls

BB1

conf t

&nbsp;

mpls label protocol ldp

router ospf 1
mpls ldp sync

interface FastEthernet0/0
ip mpls

interface FastEthernet1/0
ip mpls

BB1 Router Output

%LDP-5-NBRCHG: LDP Neighbor 3.3.3.3:0 (1) is UP
%LDP-5-NBRCHG: LDP Neighbor 2.2.2.2:0 (2) is UP

&nbsp;

Now lets add a customer to our MPLS

<img class="alignnone size-medium wp-image-296" src="http://frankmancuso.ca/wp-content/uploads/2019/08/mpls2-300x78.jpg" alt="" width="300" height="78" />

I called the Routers PEPSI_R1 and PEPSI_R2

&nbsp;

Lets configure OSPF for the customer PEPSI than I will add another customer using EIGRP so you can see how the different Routing Protocols are configured.

PE1

conf t

ip vrf PEPSI
rd 2:2
route-target both 2:2
exit

interface FastEthernet1/0
ip vrf forwarding PEPSI
ip address 192.168.1.1 255.255.255.0
ip ospf 2 area 2

PEPSI_R1

&nbsp;

interface FastEthernet0/0
ip address 192.168.1.2 255.255.255.0
ip ospf 2 area 2

%OSPF-5-ADJCHG: Process 2, Nbr 192.168.1.1 on FastEthernet0/0 from LOADING to FULL, Loading Done

Now you can verify you can ping PE1 and also that it is your neighbor

PEPSI_R1#ping 192.168.1.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 4/7/8 ms

PEPSI_R1#show ip ospf neighbor

Neighbor ID Pri State Dead Time Address Interface
192.168.1.1 1 FULL/DR 00:00:39 192.168.1.1 FastEthernet0/0

&nbsp;

If you want to ping from PE1 you would have to execute ping like this

PE1#ping vrf PEPSI 192.168.1.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 4/76/192 ms

&nbsp;

Now lets get other PEPSI side up

PE2

&nbsp;

conf t

ip vrf PEPSI
rd 2:2
route-target both 2:2
exit

interface FastEthernet0/0
ip vrf forwarding PEPSI
ip address 192.168.2.1 255.255.255.0
ip ospf 2 area 2

&nbsp;

&nbsp;

PEPSI_R2

interface FastEthernet0/0
ip address 192.168.2.2 255.255.255.0
ip ospf 2 area 2

&nbsp;

%OSPF-5-ADJCHG: Process 2, Nbr 192.168.2.1 on FastEthernet0/0 from LOADING to FULL, Loading Done

&nbsp;

Now after you have verified PE2 and PEPSI_R2 are working

PEPSI_R2#ping 192.168.2.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.2.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 20/52/148 ms

&nbsp;

PEPSI_R2#show ip ospf neighbor

Neighbor ID Pri State Dead Time Address Interface
192.168.2.1 1 FULL/BDR 00:00:31 192.168.2.1 FastEthernet0/0

&nbsp;

PE2#ping vrf PEPSI 192.168.2.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.2.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 20/61/148 ms

&nbsp;

Now in order for PEPSI Routers to talk we need to redistribute routes in BGP on PE1 and PE2

PE1

conf t

router bgp 65001

address-family ipv4 vrf PEPSI
redistribute ospf 2 vrf PEPSI

router ospf 2 vrf PEPSI
redistribute bgp 65001 subnets

PE2

conf t

router bgp 65001

address-family ipv4 vrf PEPSI
redistribute ospf 2 vrf PEPSI

router ospf 2 vrf PEPSI
redistribute bgp 65001 subnets

&nbsp;

Now if you do show ip route on PEPSI_R1

&nbsp;

PEPSI_R1#show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2
i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
ia - IS-IS inter area, * - candidate default, U - per-user static route
o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
+ - replicated route, % - next hop override

Gateway of last resort is not set

192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C 192.168.1.0/24 is directly connected, FastEthernet0/0
L 192.168.1.2/32 is directly connected, FastEthernet0/0
O IA 192.168.2.0/24 [110/2] via 192.168.1.1, 00:00:15, FastEthernet0/0

&nbsp;

Verify you can traceroute

PEPSI_R1#traceroute 192.168.2.2
Type escape sequence to abort.
Tracing the route to 192.168.2.2
VRF info: (vrf in name/id, vrf out name/id)
1 192.168.1.1 112 msec 56 msec 4 msec
2 10.0.1.1 [MPLS: Labels 16/19 Exp 0] 88 msec 56 msec 52 msec
3 192.168.2.1 80 msec 44 msec 60 msec
4 192.168.2.2 108 msec 64 msec 84 msec

&nbsp;

PEPSI_R2#traceroute 192.168.1.2
Type escape sequence to abort.
Tracing the route to 192.168.1.2
VRF info: (vrf in name/id, vrf out name/id)
1 192.168.2.1 20 msec 76 msec 20 msec
2 10.0.2.1 [MPLS: Labels 17/19 Exp 0] 52 msec 52 msec 52 msec
3 192.168.1.1 60 msec 44 msec 52 msec
4 192.168.1.2 72 msec 56 msec 84 msec

&nbsp;

Now lets add another customer who is using EIGRP

&nbsp;

<img class="alignnone size-medium wp-image-302" src="http://frankmancuso.ca/wp-content/uploads/2019/08/mpls-3-300x87.jpg" alt="" width="300" height="87" />

For this example we will use the same IP block cause there are many chances that customers will share the same IP network.

&nbsp;

PE1

conf t

ip vrf COKE
rd 100:100
route-target both 100:100

interface FastEthernet1/1
ip vrf forwarding COKE
ip address 192.168.1.1 255.255.255.0

router eigrp 100

address-family ipv4 vrf COKE autonomous-system 100

network 192.168.1.0 0.0.0.255

no auto-summary

&nbsp;

COKE_R1

conf t

interface FastEthernet0/0
ip address 192.168.1.2 255.255.255.0

router eigrp 100
network 192.168.1.0

Now you will see on COKE_R1 eigrp neighbor form.

%DUAL-5-NBRCHANGE: EIGRP-IPv4 100: Neighbor 192.168.1.1 (FastEthernet0/0) is up: new adjacency

&nbsp;

Lets configure other Coke Router

&nbsp;

PE2

conf t

ip vrf COKE

rd 100:100

route-target both 100:100

interface FastEthernet1/1
ip vrf forwarding COKE
ip address 192.168.2.1 255.255.255.0

&nbsp;

router eigrp 100

address-family ipv4 vrf COKE autonomous-system 100

network 192.168.2.0 0.0.0.255

no auto-summary

&nbsp;

COKE_R2

conf t

interface fastEthernet 0/0

ip address 192.168.2.2 255.255.255.0

&nbsp;

router eigrp 100

network 192.168.2.0 0.0.0.255

no auto-summary

&nbsp;

COKE_R2 now has EIGRP neighbor

%DUAL-5-NBRCHANGE: EIGRP-IPv4 100: Neighbor 192.168.2.1 (FastEthernet0/0) is up: new adjacenc

&nbsp;

Lets redistribute EIGRP into BGP and BGP into EIGRP so both Coke Routers can talk.

&nbsp;

&nbsp;

PE1

&nbsp;

conf t

&nbsp;

router bgp 65001

&nbsp;

address-family ipv4 vrf COKE

redistribute eigrp 100

&nbsp;

router eigrp 100

address-family ipv4 vrf COKE

redistribute bgp 65001 metric 100 1 255 1 1500

&nbsp;

PE2

router bgp 65001

&nbsp;

address-family ipv4 vrf COKE

redistribute eigrp 100

&nbsp;

router eigrp 100

address-family ipv4 vrf COKE

redistribute bgp 65001 metric 100 1 255 1 1500

&nbsp;

Now lets verify Coke routers can route

COKE_R1#show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2
i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
ia - IS-IS inter area, * - candidate default, U - per-user static route
o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
+ - replicated route, % - next hop override

Gateway of last resort is not set

192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C 192.168.1.0/24 is directly connected, FastEthernet0/0
L 192.168.1.2/32 is directly connected, FastEthernet0/0
D 192.168.2.0/24 [90/30720] via 192.168.1.1, 00:00:27, FastEthernet0/0

&nbsp;

COKE_R1#traceroute 192.168.2.2
Type escape sequence to abort.
Tracing the route to 192.168.2.2
VRF info: (vrf in name/id, vrf out name/id)
1 192.168.1.1 8 msec 160 msec 136 msec
2 10.0.1.1 [MPLS: Labels 16/20 Exp 0] 84 msec 52 msec 72 msec
3 192.168.2.1 84 msec 60 msec 64 msec
4 192.168.2.2 100 msec 96 msec 76 msec

&nbsp;

COKE_R2#traceroute 192.168.1.2
Type escape sequence to abort.
Tracing the route to 192.168.1.2
VRF info: (vrf in name/id, vrf out name/id)
1 192.168.2.1 64 msec 24 msec 8 msec
2 10.0.2.1 [MPLS: Labels 17/20 Exp 0] 72 msec 52 msec 48 msec
3 192.168.1.1 68 msec 52 msec 52 msec
4 192.168.1.2 64 msec 92 msec 80 msec

&nbsp;

I hope this article will help you with your learning path.

&nbsp;

&nbsp;
