Cisco IOS Steps

Configure the following on the interface you want to capture netflows on. Most cases you would enable on WAN and LAN

```
interface gig0/0/0
description WAN
ip nbar protocol-discovery
ip flow ingress</code>
```

```
interface gig0/0/1
description LAN
ip nbar protocol-discovery
ip flow ingress
```

Now Configure your Flow Exporter

You will export to your netflow server via the LAN interface unless its cloud based.

```
ip flow-export source GigabitEthernet0/0/1
```

Change the IP address and the port destination

```
ip flow-export destination 192.168.1.5 9999
```


Cisco IOS XE is a lot different to configure NetFlow here are the steps

First let configure our netflow exporter
```
flow exporter netflow
destination 192.168.1.5
source GigabitEthernet0/0/1
transport udp 9999
export-protocol netflow-v5
```

Now Let configure the netflow Monitor

```
flow monitor netflow
exporter netflow
record netflow-original
```

Now configure your interfaces

```
Interface gig0/0/0
description WAN
ip flow monitor netflow input
ip nbar protocol-discovery
```

```
Interface gig0/0/1
description LAN
ip flow monitor netflow input
ip nbar protocol-discovery
```
