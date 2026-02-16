# EIGRP_Network_Lab
This lab is about configuring three different networks using the Enhanced Interior Gateway Routing Protocol (EIGRP)to help routers share routes and allow all devices in the networks to communicate with each other.


# This lab is about configuring three different networks using the Enhanced Interior Gateway Routing Protocol (EIGRP) to help routers share routes and allow all devices in the networks to communicate with each other.

<img width="975" height="518" alt="image" src="https://github.com/user-attachments/assets/368d9a9a-d806-441e-b0ce-756379482cdb" />





## I am configuring Router1 by assigning its IP address and subnet mask.



Router1(config)#int gi0/0/0

Router1(config-if)#ip address 192.168.1.254 255.255.255.0

Router1(config-if)#des

Router1(config-if)#description connected SW1

Router1(config-if)#no shut


Router1(config-if)#

%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up


Router1#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Router1(config)#int gi0/0/1

Router1(config-if)#ip address 10.255.255.253 255.255.255.0

Router1(config-if)#de

Router1(config-if)#des

Router1(config-if)#description connected R2

Router1(config-if)#no shut

## I am configuring Router2 by assigning its IP address and subnet mask.
 connected Sw2

R2#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

R2(config)#interface gi0/0/0

R2(config-if)#des

R2(config-if)#description  connected SW2

R2(config-if)#ip address 172.168.15.254 255.255.255.0

R2(config-if)#no shut


R2(config-if)#

%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up


%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up


R2(config-if)#end

R2#

%SYS-5-CONFIG_I: Configured from console by console


R2#copy run start

Destination filename [startup-config]? 

Building configuration...

[OK]


Router>en


Router# conf t


Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#host

Router(config)#hostname R2

R2(config)#interface gi0/0/1

R2(config-if)#ip address 10.255.255.254 255.255.255.0

R2(config-if)#desc

R2(config-if)#description connected R1

R2(config-if)#no shut


R2(config-if)#

%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up


%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up


## Initiate a ping from PC1 to Router1 to verify connectivity between the end device and the gateway.


Cisco Packet Tracer PC Command Line 1.0



C:\>ping 192.168.1.254


Pinging 192.168.1.254 with 32 bytes of data:


Reply from 192.168.1.254: bytes=32 time<1ms TTL=255

Reply from 192.168.1.254: bytes=32 time=1ms TTL=255

Reply from 192.168.1.254: bytes=32 time=1ms TTL=255

Reply from 192.168.1.254: bytes=32 time<1ms TTL=255


Ping statistics for 192.168.1.254:

    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

Minimum = 0ms, Maximum = 1ms, Average = 0ms

## Initiate a ping from PC1 to the server to test network connectivity.


C:\>ping 172.16.15.10

Pinging 172.16.15.10 with 32 bytes of data:


Reply from 192.168.1.254: Destination host unreachable.

Reply from 192.168.1.254: Destination host unreachable.

Reply from 192.168.1.254: Destination host unreachable.

Reply from 192.168.1.254: Destination host unreachable.

Ping statistics for 172.16.15.10:

Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)


## The destination is currently unreachable because the network requires an internal routing protocol, such as Enhanced Interior Gateway Routing Protocol (EIGRP), to be configured.


## Configure Router1 to participate in the Enhanced Interior Gateway Routing Protocol (EIGRP) routing process.


Router#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#router ei

Router(config)#router eigrp 20

Router(config-router)#network 192.168.1.0 0.0.0.255

Router(config-router)#network 10.255.255.252 0.0.0.3

Router(config-router)#network 172.16.15.0 0.0.0.255

Router(config-router)#no au

Router(config-router)#no auto-summary 

Router(config-router)#


## Configure Router2 to participate in the Enhanced Interior Gateway Routing Protocol (EIGRP)routing process.



R2#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

R2(config)#router ei

R2(config)#router eigrp 20

R2(config-router)#network 192.168.1.0 0.0.0.255

R2(config-router)#network 10.255.255.252 0.0.0.3

R2(config-router)#

%DUAL-5-NBRCHANGE: IP-EIGRP 20: Neighbor 10.255.255.253 (GigabitEthernet0/0/1) is up: new adjacency

R2(config-router)#network 172.16.15.0 0.0.0.255

R2(config-router)#no au

R2(config-router)#no auto-summary 

R2(config-router)#

%DUAL-5-NBRCHANGE: IP-EIGRP 20: Neighbor 10.255.255.253 (GigabitEthernet0/0/1) resync: summary configured



## To verify that the configuration is functioning correctly, initiate a **ping** from **PC1** to the server.


 
C:\>ping 172.16.15.10


Pinging 172.16.15.10 with 32 bytes of data:


Reply from 172.16.15.10: bytes=32 time=1ms TTL=126

Reply from 172.16.15.10: bytes=32 time<1ms TTL=126

Reply from 172.16.15.10: bytes=32 time=10ms TTL=126

Reply from 172.16.15.10: bytes=32 time<1ms TTL=126

Ping statistics for 172.16.15.10:

    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

 Minimum = 0ms, Maximum = 10ms, Average = 2ms



## Navigate to the opposite side of the network and initiate a **ping** from the server to **PC2** to verify end-to-end connectivity.


C:\>ping 192.168.1.10


Pinging 192.168.1.10 with 32 bytes of data:


Reply from 192.168.1.10: bytes=32 time<1ms TTL=126

Reply from 192.168.1.10: bytes=32 time<1ms TTL=126

Reply from 192.168.1.10: bytes=32 time<1ms TTL=126

Reply from 192.168.1.10: bytes=32 time<1ms TTL=126


Ping statistics for 192.168.1.10:

 Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

    Minimum = 0ms, Maximum = 0ms, Average = 0ms


## Both sides of the network are now successfully communicating using the EIGRP protocol, ensuring full route exchange and network connectivity.

