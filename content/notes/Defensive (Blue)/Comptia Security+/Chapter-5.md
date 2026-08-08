typical weakness in a network architecture include 
- single points of failure 
- complex dependencies 
- availability over confidentiality and integrity 
- lack of documentation and change control 
- overdependence on perimeter security 
# Switches 
they work at layer 2 of the OSI model and make forwarding messages based on the hardware or 'media access control' (mac) address of attached nodes 
they can establish network segments that either map directly to the underlying cabling or to logical segments created in the switch configuration as Virtual LANs 
# Wireless Access Points 
provide a bridge between a cabled network and wireless clients or stations , work at layer 2 of OSI model 
# Load Balancers 
distribute traffic between network segments or servers to optimize performance . they work at layer 4 of OSI model 
# Routers 
forward packets around an internetwork , making forward decision based on 'IP addresses' , work at layer 3 of the OSI model 
they can apply logical IP subnet addresses to segments within a network 
# Firewalls
They apply an access control list (ACL) to filter traffic passing in or out of a network segment . works at layer 3 of the OSI model 
# Domain Name System (DNS) Servers
hostname records and perform name resolution to allow applications and users to address hosts and services using fully qualified domain names rather than IP addresses , works at layer 7 of the OSI model 
# Network Segmentation 
one where all the hosts attached to the segment can use local forwarding to communicate freely with one another 
@segregation - means that the hosts in one segment are restricted in the way they communicate with hosts in other segments 
@freely - means that no network appliances or policies are preventing communications 
# Network Topology & Zones 
description of how a computer network is physically or logically organized 
the main building block of a topology is a 'zone' which is an area of the network where the security configuration is the same for all hosts within it 
'zones' can be segregated with VLANs while the traffic between them can be controlled using a security device typically a firewall 
# Network Zones 
- intranet (private network) - this is a network of trusted hosts owned and controlled by the organization 
- extranet - network of semi-trusted hosts typically representing business parties , suppliers or customers
- internet/guest - this is a zone permitting anonymous access by untrusted hosts over the internet 
# Demilitarized Zones (DMZs) 
in a dmz , external clients are allowed to access data on private systems such as web servers without compromising the security of the internal network as a whole 

if communcation is required between hosts on either side of a dmz , a host within the dmz acts as a proxy 
the hosts in a dmz are not fully trusted and are referred to as "bastion hosts" and run minimal services to reduce the attack surface as much as possible

two different security config must be enabled - 1. internal 2. external , a dmz and intranet are on different subnets so communications between them need to be routed 

@Screened Subnet 
two firewalls placed on either side of the DMZ , edge firewall restricts traffic on the external/public interface and allows permitted traffic to the hosts in the DMZ 

the internal firewall filters communication between hosts in the dmz and hosts on the lan , also called "choke" firewall 

small networks may not have the budget to implement a dmz , internet access can still be implemented using a dual-homed proxy/gateway server acting as a screened host , solves the access problems but vulnerable to intrusion and Dos attacks 
# east-west traffic 
traffic that goes to and from a data center is referred to as north-south . this traffic represents clients outside the data center making requests 
however , data centers that support cloud services , most traffic is actually between servers within that data center and this traffic is referred to as "east-west" traffic 
# zero trust
perimeter security is unlikely to be robust enough so continuous authentication and conditional access are used to mitigate threats 
*Microsegmentation* - a security process that is capable of applying policies to a single node as though it was in a zone of its own
# routing and switching protocols 
network - to forward traffic from one node to another 
forwarding function takes place at two different layers 
@layer2 - forwarding occurs between nodes on the same local network segment that are all in the same broadcast domain . each node is identified by the mac address 
@layer3 - routing occurs between both logically and physically defined networks , single network divided into multiple logical broadcast domains is said to be "subnetted" . nodes are identified by ip addresses
# arp (address resolution protocol) 
maps mac address to an ip address 
when a device needs to send a packet to an ip address but does not know the receiving device's mac address , broadcasts will broadcast an arp request packet and the device with the matching ip responds with an arp reply 
# ip (internet protocol)
provides the addresssing mechanism for logical networks and subnets 
*172.16.1.101/16*
/16 prefix indicates that the first half of the address (172.16.0.0) is the network ID while the remainder uniquely identifies a host on that network 
networks also use 128-bit IPv6 addressing 
*2001:db8:abc:0:def0:1234* 
the first 64 bits contain network information while the last are fixed as the host's interface ID 
# routing protocols
route to a network can be configured statically but most networks use routing protocols to transmit new and updated routes between routers , some protocols - 
- border gateway protocol (bgp) 
- open shortest path first (ospf)
- enhanced interior gateway routing protocol (eigrp) 
- routing information protocol (rip) 
# man-in-the-middle & layer 2 attacks 
most attacks at layer 1 and 2 of the OSI model are typically focused on information gathering through "network mapping" and "eavesdropping" 
at mitm can also be performed on this layer due to the lack of security 
*mac cloning* or *mac address spoofing* changes the hardware address of an adapter to an arbitrary one either by overriding the original address in software via OS commands or with the use of packet crafting software 
# arp poisoning attack 
this attack uses packet crafter such as 'ettercap' to broadcast unsolicited arp reply packets cuz arp has no security mechanism , the receiving devices trust this communication and update their MAC:IP address cache table with the spoofed address 
# mac flooding attacks 
arp poisoning is directed at hosts , mac flooding is used to attack a switch , the idea here is to exhaust the memory used to store the switch's MAC address table which is used by the switch to determine which port to use to forward unicast traffic to its correct destination 
overwhelming the table can cause the switch to stop trying to apply MAC-based forwarding and simply flood unicast traffic out of all ports 
# loop prevention 
layer 2 broadcast traffic could potentially continue to loop through a network with multiple paths indefinitely but this is prevented by the "spanning tree protocol" , stp is a means for the bridges to organize themselves into a hierarchy and prevent loops from forming 
stp is designed to prevent "broadcast storms" which is traffic that is recirculated and amplified by loops in a switching topology causing network slowdowns and crashing switches 
# router/switch security 
- physical port security - access to physical switch ports and hardware should be restricted to authorized staff by using a secure server room or lockable hardware cabinets
- mac filtering & mac limiting - configuring mac filtering on a switch means defining which mac addresses are allowed to connect to a particular port by creating a list of valid mac addresses . mac limiting involves specifying a limit to the number of permitted addresses that can connect to a port 
- dhcp snooping - dynamic host configuration protocol is one that allows a server to assign an ip address to a client when it connects to a network . dhcp snooping inspects this traffic arriving an access ports to ensure that a host is not trying to spoof its mac address . with dhcp snooping only dhcp messages from ports configured as trusted are allowed 
# network access control
- the IEEE 802.1X standard defines a port based network access control (pnac) mechanism 
- pnac means that the switch uses an AAA server to authenticate the attached device before activating the port 
- nac products can extend the scope of authentication to allow admins to revise policies or profiles , describing a minimum security configuration that devices must meet to be granted network access . this is called a "health policy" 
- typical policies might check for malware infection , presence of a firewall and an up-to-date anti-malware. software 
- "Posture assessment" is the process by which host health check are performed against a client device to verify compliance with the health policy 
- most nac solutions use client software called an "agent" to gather info about the device . agents can be persistent(installed on the client) or nonpersistent (loaded into memory during posture assessment) 
# route security
a successful attack against route security enables the attacker to redirect traffic from its intended destination 
routes between networks and subnets can be configured manually , but most routers automatically discover routes by communicating with each other 
vulnerabilities --
- spoofed routing info (route injection) - traffic is misdirected to a monitoring port (sniffing) or continuously looped around the network causing DoS
- routers can be configured to identify the peers from which it will accept route updates from
- software exploits in the underlying os - Cisco devices typically use the internetwork operating system (ios) which suffer from fewer exploitable vulnerabilities than full network os
# Packet Filtering Firewalls 
the earliest type of firewalls and are configured by specifying a group of rules called an access control list (ACL) 

each rule defines a specific type of data packet and the appropriate action to take when a packet matches the rule , an action can either deny or to accept the packet. 
This firewall can inspect the headers of ip packets --> 
- ip filtering - accepting/denying traffic based on source/destination ip address
- protocol id (tcp, udp, icmp etc)
- port filtering - accepting/denying on source/destination port numbers 
firewall can control 
@ingress - inbound traffic 
@egress - inbound + outbound traffic {useful cuz it block apps that have not been authorized to run on the network and defeat malware such as backdoors}

basic packet filtering firewall is "stateless" meaning that it does not preserve any information about network sessions , the least processing effort is required for this but it can be vulnerable to attacks that are spread over a sequence of packets 
# Stateful Inspection Firewalls
this firewall can track info about the session b/w 2 hosts and the session data is stored in a "state table" , when a packet arrives , the firewall checks if belongs to existing connections , if does then allowed to pass unmonitored to conserve processing effort 
# Transport Layer (Layer -4)
firewall examines tcp 3 way-handshakes to distinguish new from established connections 
SYN>SYN/ACK>ACK
any deviations from this sequence can be dropped as ==malicious flooding== or ==session hijacking== attempts 
# Application Layer (Layer -7)
this firewall inspects contents of the packets at the application layer , and one key feature is to verify the application protocol matches the port 
eg - http web traffic will use port 80

it cannot examine encrypted data packets unless configured with an SSL/TLS inspector 
# IP Tables 
a command on linux that allows admins to edit the rules enforced by the linux kernel firewall . ip tables works with chains which apply to the different types of traffic such as the INPUT chain of traffic destined for the local host . each chain hash a default policy set to DROP or ALLOW traffic that does not match a rule 

the command `iptables --list INPUT --line-numbers -n`will show the contents of the INPUT chain with line numbers and no name resolution 

the 'ctstate' rule is a stateful rule that allows any traffic that is part of an established or related session 
# Firewall Appliances 
a stand-alone firewall deployed to monitor traffic passing into and out of a network zone 
can be deployed in 2 ways -->
- Routed (layer-3) - the firewall performs forwarding between subnets 
- Bridged (Layer-2) - the firewall inspects traffic between two nodes such as a router and a switch 
# Router Firewall 
implements filtering functionality as part of the router firmware 
# Application Firewall
- Host based (personal) - implemented as a software application designed to protect the host only 
- Application Firewall - software designed to run on a server to protect a particular application only 
- Network Operating System (NOS) firewall - software based firewall running under a network server OS such as Windows or Linux
# Proxies and Gateways 
firewall that performs application layer filtering is likely to be implemented as a proxy , a *forward* proxy server provides for protocol specific "outbound" traffic 

proxy can be -
- non-transparent - means the client must be configured with the proxy server address and port number to use it 
- transparent - intercepts client traffic without the client having to be reconfigured 
# Reverse Proxy Servers 
- for security purposes you may not want external hosts to communicate directly with application servers like web or email 
- a reverse proxy can be deployed on the network edge and configured to listen for client requests from a public network 
# UTM (unified threat management)
a security product that centralizes many types of security controls - firewall , antimalware , spam filtering , vpn etc into a single appliance 

the downside is that this creates a single point of failure that can affect the entire network , they can also struggle with latency issues if they are subject to too much network activity 
# Content/URL filter 
a content filter is designed to apply a number of user-focused filtering rules such as applying time-based restrictions to browsing , also are now implemented as a class of product called "secure web gateway (swg)" which can also integrate filtering with the functionality of data loss prevention 
# Host-Based IDS
hids captures info from a single host , the core ability is to capture and analyze log files but more sophisticated systems can also monitor os kernel files, monitor ports and network interfaces 
@fim (file integrity monitoring)- this software will audit key systems files to make sure they match the authorized versions 
# Web Application Firewall (WAF)
designed to specifically protect software running on web servers and their back-end databases from code injection and DOS attacks 
they use app-aware processing rules to filter traffic and perform app-specific intrusion detection  
# Remote Access Architecture 
p2p tunneling protocol has been deprecated while TLS and IPSec are now the preferred options for configuring VPN access , a *tls vpn* (ssl vpn) requires a remote access server listening on port 443 
# Transport Layer Security VPN
client makes a connection to the server using tls so that the server is authenticated to the client . this creates an encrypted tunnel for the user to submit authentication credentials which would normally be processed by a RADIUS server , once the user is authenticated and the connection fully established the vpn gateway tunnels all communications for the local network over the secure socket 
# Open VPN
can work in TAP(bridged) mode to tunnel layer 2 frames or TUN(routed) mode to forward ip packets . another option is microsoft's secure sockets tunneling protocol (sstp) which works by tunneling point-2-point protocol(ppp) layer 2 frames over a tls session 
# Internet Protocol Security (IPSec)
tls is applied at the application level either by using a separate secure port or by using commands in the application protocol to negotiate a secure connection 

ipsec operates at the network layer (layer-3) so it can operate without having to configure specific application support 

ipsec can provide confidentiality by encrypting data packets and integrity by signing each packet although it does add some overhead to data communications , 2 protocols in ipsec-
- authentication header 
- encapsulation security payload 
@authentication header - performs cryptographic hash on the whole packet including the ip header plus a shared secret key and adds this HMAC in its header as *integrity check value* 

the recipient performs the same function on the packet and key and should derive the same value to confirm that the packet has not been modified 

@encapsulation security payload - provides confidentiality or authentication and integrity . it can be used to encrypt the packet rather than simply calculating an HMAC

esp attaches three fields to the packet a header , a trailer (providing padding for the cryptographic function) and an icv 
# IPSEC transport and tunnel modes 
- transport mode - this mode is used to secure communication between hosts on a private network , here the ip header for each packet is not encrypted just the payload data 
![[Pasted image 20260808122156.png]]
if ah is used in this mode , it can provide integrity for the ip header 
- tunnel mode - this mode is used for communications between VPN gateways across an unsecure network and is also referred to as router implementation
![[Pasted image 20260808122410.png]]
with esp , the whole ip packet (header and payload) is encrypted and encapsulated as a datagram with a new ip header 
# Internet Key Exchange (IKE)
ipsec's encryption and hashing functions depend on a shared secret , this secret must be communicated to both hosts and the hosts must confirm one another's identity (mutual authentication) otherwise the connection is vulnerable to MITM and spoofing attacks 
ike negotiations take place over 2 phases : 
- phase 1 - establishes the identity of the two hosts and performs key agreement using the DH algo to create a secure channel . digital certificates and pre shared key are used for authentication hosts 
- phase 2 - uses the secure channel created in phase1 to establish which ciphers and key sizes will be used with AH and/or ESP in the IPSec session 
# Layer 2 tunneling protocol and ike v2
1st version of ike is optimized to ensure the mutual authentication of 2 peer hosts such as in a site-to-site VPN however for remote access VPNs , combo of IPSec with L2TP VPN protocol is often used 

L2TP typically operate as follows - 
1. the client and VPN gateway set up a secure IPSec channel over the internet using either a pre shared key or certificates for ike 
2. the VPN gateway uses L2TP to set up a tunnel to exchange local network data encapsulated as PPP frames 
3. the user authenticates over the PPP session using EAP or CHAP
# IKE V2
some additional features - 
- support for EAP authentication methods 
- simplified connection set up
- reliability 
IKE V2 is more efficient than L2TP/IPSec
# VPN Client Configuration 
may need to install the client software if the VPN type is not natively supported by the OS 
# Always on VPN
means computer establishes the VPN whenever an internet connection over a trusted network is detected using the user's cached credentials to authenticate 
# Split tunnel vs Full tunnel
- split tunnel - the client accesses the internet directly using its 'native ip' config and dns servers 
- full tunnel - internet access  is mediated by the corporate network, which will alter the client's ip address and dns servers and may use a proxy , full tunnel offers better security but the network address translations and DNS operations required may cause problems with some websites especially cloud services 
# Remote Desktop 
microsoft's remote desktop protocol (rdp) can be used to access a physical machine on a one-to-one basis 
other alternatives inc team viewer and virtual network computing (vnc) which are implemented by different providers 

**html5 vpn** - a secure remote access solution that allows users to connect to internal corporate networks and applications directly through a modern web browser
# out-of-band management 
**in band** management link is one that shares traffic with other communications on the 'production' network while a serial console or modem port on a router is a physically **out of band** management method 

oob management is more secure and means that access to the device is preserved when there are problems affecting the production network 

with an in band connection , better security can be implemented by using a VLAN to isolate management traffic 
# jump servers 
hosts exposed to the internet (ie dmz or cloud virtual network) , is to provide secure admin access to the servers and appliances located within it , configuring and auditing control when there are many different servers operating in the zone can be very complex 

**solution** - add a single administration server/ jump server to the secure zone . it only runs the necessary admin port and protocol and the admins can connect to the jump server then use it to connect to the admin interface on the application server 

the admin interface has a single entry in its ACL and denies connection attempts from any other hosts 
# Secure Shell (ssh) 
this is the principal means of obtaining secure remote access to a command line terminal , mostly used for remote administration and secure file transfer (sftp) 
- ssh servers are identified by a public/private key pair (the host key) 
# ssh client authentication 
- username/password - client submits creds that are verified by the ssh server either against a local user database or using a RADIUS/TACACS+ server 
- public key authentication - each remote user's public key is added to a list of keys authorized for each local account on the ssh server 
- kerberos - the client submits the kerberos credentials obtained when the user logged onto the workstation to the server using GSSAPI (generic security services application program interface) 
# ssh commands 
ssh server at - 10.1.0.10 using account named - "bobby" and password authentication , run 
```bash
ssh bobby@10.1.0.10
```
the below command create a new key pair and copy it to an account on the remote server 
```bash
ssh-keygen -t rsa 
ssh-copy-id bobby@10.1.0.10
```
`scp` command to copy a file from the remote server to the local host 
```bash
scp bobby@10.0.1.10:logs/audit.log audit.log 
```
