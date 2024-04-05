---
layout: post
title:  "A list of fundamental concepts of Network"
date:   2024-04-02
categories: foundation
permalink: /:categories/intro-network
---


<p>Here we have only brief concepts as introduction of network.</p>

<p>
  <center>
      <img src="/img/architecture/networkcomponent.png" width="50%" height="50%"/><br />
      <em>Source: <a href="https://digitalthinkerhelp.com/what-is-basic-hardware-components-devices-of-computer-network/?utm_content=cmp-true">digitalthinkerhelp.com</a></em>
  </center>
</p>

<br />
<h2>Short notes of network</h2>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/products/switches/what-is-a-lan-local-area-network.html"><b>[LAN]</b></a>A local area network (LAN) is a collection of devices connected together in one physical location, such as a building, office, or home.</p>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/products/switches/what-is-an-ethernet-switch.html"><b>[Ethernet switch]</b></a> is a type of network hardware that is foundational to networking and the internet. It avoid collision problems. It is a hub + bridge. It has MAC table.</p>

<p style="text-align: justify;"><a href="https://en.wikipedia.org/wiki/MAC_address"><b>[MAC]</b></a> is the physical address (Unique Layer 2 address given to every network interface on an Ethernet network). Commands: ifconfig or ipconfig.</p>

<p style="text-align: justify;"><a href=""><b>[NIC]</b></a> Network Interface Cards is a hardware in a computer that provides an Ethernet port. It has unique MAC address.</p>

<p><a href="https://www.cbtnuggets.com/blog/technology/networking/what-is-ethernet-frame-format"><b>[Ethernet frame]</b></a> is involved in the communication between two machines. It is source mac + mac destiny + payload</p>

<p style="text-align: justify;"><a href="https://www.geeksforgeeks.org/what-is-network-hub-and-how-it-works/"><b>[Hub]</b></a> device to connect ports but it is dumb. Send the frame to everyone. Open to collision</p>

<p style="text-align: justify;"><a href="https://geek-university.com/what-is-a-network-bridge/">[Bridge]</a> decide for who avoiding colision. It use MAC tables</p>

<p style="text-align: justify;"><a href="https://www.geeksforgeeks.org/difference-between-unicast-broadcast-and-multicast-in-computer-network/">[Unicast vs Multicast vs Broadcast]</a> is the way of transmition of data.</p>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/what-is-a-router.html"><b>[Router]</b></a> guide and direct network data. It is connected to a switch on a trunk port. Trunk port is a network port on a switch that can carry traffic for multiple VLANs. I break up broadcast segments.</p>

<p style="text-align: justify;"><a href="https://www.geeksforgeeks.org/routing-tables-in-computer-network/"><b>[Route Table]</b></a> is a set of rules used to identify the direction to send the data packets over network.</p>

<p style="text-align: justify;"><a href="https://networklessons.com/cisco/ccna-routing-switching-icnd1-100-105/what-is-subnetting"><b>[Subnet]</b></a> is a sub-network of a network.</p>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/products/routers/what-is-a-network-gateway.html"><b>[Network gateway]</b></a> is a device or node that connects disparate networks by translating communications from one protocol to another. Routers are default gateways for devices within their segments.</p>

<p style="text-align: justify;"><a href="https://www.guru99.com/vlan-definition-types-advantages.html"><b>[VLAN]</b></a> is a custom network which is created from one or more local area networks. It avoid many physical switches. Logical segmentation. Each LAN has a subnet. VLANs are inside to swiche. Use router to communicate among the VLANs.</p>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/products/switches/what-is-a-wan-wide-area-network.html"><b>[WAN]</b></a> (wide-area network) is a collection of local-area networks (LANs) or other networks that communicate with one another.  Connect router of different and distant network. Router use WAN interface and send message to neighbors or sent to internet (0.0.0.0/0 -> data centers).</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/what-is/border-gateway-protocol/"><b>[BGP]</b></a> (Border Gateway Protocol) is a set of rules that determine the best network routes for data transmission on the internet.</p>

<p style="text-align: justify;"><a href="https://docs.paloaltonetworks.com/network-security/ipsec-vpn/administration/ipsec-vpn-basics/ipsec-vpn"><b>[IPSEC VPN]</b></a> provides a private and secure IP communication over a public network. Public IP using securely tunnel with secrets.</p>

<p style="text-align: justify;"><a href="https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000/l2vpn/75x/b-l2vpn-cg-cisco8000-75x/m-introduction-to-layer-2-vpns.pdf"><b>[Layer 2 VPN]</b></a> emulates a physical sub-network in an IP or MPLS network, by creating private connections between two points. It extends Layer 2 network segments over geographic distance. It establish a secure VPN tunnel</p>

<p style="text-align: justify;"><a href="https://www.trgdatacenters.com/resource/what-is-network-redundancy/"><b>[Redundancy]</b></a> ensure the continuous operation. Multiple router. It should eliminate the SPOF (single point of failure). Strategy: Redundant Component, Redundant Path, Protocols as <a href="https://www.cisco.com/c/en/us/support/docs/ip/hot-standby-router-protocol-hsrp/9234-hsrpguidetoc.html">HSRP</a> or <a href="https://www.geeksforgeeks.org/introduction-of-virtual-router-redundancy-protocol-vrrp-and-its-configuration/">VRRP</a>, Dybamic Routing such as <a href="https://www.geeksforgeeks.org/open-shortest-path-first-ospf-protocol-states/">OSPF</a> or BGP.</p>

<p style="text-align: justify;"><a href="https://learn.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top"><b>[DHCP]</b></a>: Dynamic Host Protocol. When a machine issues a DHCP (Dynamic Host Configuration Protocol) request, it typically sends an Ethernet broadcast message on the local network. This broadcast is used to discover and contact a DHCP server within the network, requesting an IP address assignment and other network configuration information.</p>

<p style="text-align: justify;"><a href="https://www.youtube.com/watch?v=QTu7yDnR_58&list=PLTk5ZYSbd9MhMmOiPhfRJNW7bhxHo4q-K&index=2">[DNS]</a> Domain Name System (nslookup www.google.com -> DNS query to find the IP address)</p>

<p style="text-align: justify;"><a href="https://www.geeksforgeeks.org/network-address-translation-nat/"><b>[NAT]</b></a> (Network Address Translation) has the idea that multiple devices access the Internet through a single public address. It is a networking technique that modifies network address information in data packets as they pass through a router or firewall, allowing multiple devices within a local network to share a single public IP address for communication with external networks like the internet. This process helps conserve public IP addresses and adds a layer of security by hiding internal network structures from external sources.</p>

<p><a href="https://www.meridianoutpost.com/resources/articles/IP-classes.php"><b>[NTP]</b></a>: Network Time Protocol </p>

<p style="text-align: justify;"><a href="https://www.networkacademy.io/ccna/ip-subnetting/what-is-vlsm"><b>[VLSM]</b></a>: (Variable Length Subnet Masking) the primary puerpose if to allocate IP address more efficiently by allowing for different subnet sizes within the same network.</p>

<br />
<h2>Layer <a href="https://www.fortinet.com/resources/cyberglossary/tcp-ip-model-vs-osi-model">[OSI vs TCP Model]</a></h2>

<table>
  <tr>
    <td>L5,6,7: Application (Session, Presentation)</td>
    <td>provide interface between the communication software and applications > communication protocol > browser > payload > protocol (http,dns, ftp, ntp, pop3, smtp, ssh, ldap, ssh)</td>
  </tr>
  <tr>
    <td>L4: Transport</td>
    <td> host to host communication layer >define protocols > Error Recovery (check data, negociation) > Flow control > 3Ways handshake (sequence number, SYN, ACK) > Protocol (TCP, UDP, RSVP) > Device (Hosts, Firewalls) > Segment (header for data, use source and destination)</td>
  </tr>
  <tr>
    <td>L3: Network</td>
    <td>Define the way for our data to communicate to devices across network (touted) > upload , IP address, networkd address > Routers and switches > Protocols (IP, ICMP - routed / OSPF, RIPv2 - routing are protocols between routers) > routing tables > Packet - data encapisuation header</td>
  </tr>
  <tr>
    <td>L2: DataLink</td>
    <td>define rules when a device can send data, define format of the header > connect with Switch > interface mac > for where> Ethernet, Wifi, Fiber Channel... > VPN > Protocols (Ethernet, PPP, WAV, ARP) > Device - switches > Frame - encapsulates all data above it, use header. Sach L2 segment has a subnet (10.1.1.0/24). Router is a default gateway</td>
  </tr>
  <tr>
    <td>L1: Physical</td>
    <td>
      <li>physical characteristics for transmitting data</li>
      <li>phisical address</li>
      <li>connect to a cable</li>
      <li>NIC (Network Interface Cards - connect devices to LAN), Ethernet, Hub, repeater</li>
      <li>sends bits of data</li></td>
  </tr>
</table>
 
<br />
<h2>IP Adress</h2>

<p>Calculate the subnet (CIDR NOTATION) <a href="https://matt-rickard.com/how-to-calculate-a-cidr">[1]</a><a href="https://networkcalc.com/articles/cidr-notation/">[2]</a><a href="https://dev.to/rishitashaw/cidr-a-brief-overview-subnet-calculation-pfc">[3]</a></p>
<table>
  <tr>
    <td>
      10.1.1.0/24 > 10.1 is the subnet. 24 first bits are the network address (10.1.1 or 10.1.2) and the last one will be used for the IP address<br /><br />
      10.1.0.0/16 means 10.1 or 10.2 is the network. So, can use 10.1.255.255 as IPs<br /><br />
      Network Address: 10.1.1.0<br />
      Default Gateway: 10.1.1.1<br />
      Broadcast Address: 10.1.1.255<br />
      </td>
    <td>
      Network Address: 172.16.0.0<br />
      Mask: 255.255.0.0<br />
      IP: 72.16.10.4<br />
      Broadcast Address: 172.16.255.<br />
    </td>
  </tr>
  <tr>
    <td>
      97.122.14.233/25<br />
      11111111.11111111.11111111.10000000<br />
      Network Address: 97.122.14.128/25<br />
      Briadcast Address: 97.122.14.255<br />
      (25)<br />
      Octet 2: 128(1) 64 32 16 8 4 2 1<br />
      only the position 128 but is part of the net. The other are host<br />
    </td>
    <td>
      14.25.98.12/14<br />
      11111111.11111100.00000000.00000000<br />
      Network Address: 14.24.0.0/14<br />
      Briadcast Address: 14.27.255.255<br />
      (25)<br />
      Octet 2: 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1<br />
                0  | 0 | 0 | 1 | 1 | 0 - -  -> 16 + 8 = 24<br />
                0  | 0 | 0 | 1 |1 |0 |1 | 1  -> 16 + 8 = 27<br />
    </td>
  </tr>
  <tr>
    <td>
      <li>https://www.subnet-calculator.com/</li>
      <li>https://www.calculator.net/ip-subnet-calculator.html</li>
      <li>https://www.site24x7.com/tools/ipv4-subnetcalculator.html</li>
    </td>
    <td>
      <li>https://www.tunnelsup.com/subnet-calculator/</li>
      <li>https://www.solarwinds.com/free-tools/advanced-subnet-calculator</li>
      <li>https://appuals.com/what-is-a-subnet-calculator-how-to-use-it/</li>
    </td>
  </tr>
</table>


<br />
<h3>References</h3>
<ul>
  <li><a href="https://www.udemy.com/course/networkingbasics/?couponCode=LETSLEARNNOWPP">Introduction to Computer Networking - 2 Hour Crash Course</a></li>
  <li><a href="https://www.udemy.com/course/cisco-tcpip-osi-network-architecture-models/?couponCode=LETSLEARNNOWPP">Cisco - TCP/IP & OSI Network Architecture Models</a></li>
  <li><a href="https://medium.com/@marameref/basic-networking-concepts-explained-251e3775f0fc">Basic Networking Concepts Explained</a></li>
  <li><a href="https://www.redhat.com/sysadmin/sysadmin-essentials-networking-basics">Learn the networking basics every sysadmin needs to know</a></li>
  <li><a href="https://www.technologygee.com/basic-networking-concepts-comptia-it-fundamentals-fc0-u61-2-7/">Basic Networking Concepts | CompTIA IT Fundamentals FC0-U61 | 2.7</a></li>
  <li><a href="https://en.wikipedia.org/wiki/OSI_model">OSI Model</a></li>
</ul>  


