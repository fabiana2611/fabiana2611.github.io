---
layout: post
title:  "A list of fundamental concepts of Network"
date:   2023-04-02
categories: foundation
permalink: /:categories/intro-network
---


<p>Here we have only brief concepts as introduction of network.</p>

<br />
<h2>Shot notes of networ</h2>

<p>
  <center>
      <img src="/img/architecture/networkcomponent.png" width="50%" height="50%"/><br />
      <em>Source: <a href="https://digitalthinkerhelp.com/what-is-basic-hardware-components-devices-of-computer-network/?utm_content=cmp-true">digitalthinkerhelp.com</a></em>
  </center>
</p>


<p><a href="https://en.wikipedia.org/wiki/MAC_address">MAC:</a> physical address (Unique Layer 2 address given to every network interface on an Ethernet network)</p>

<p>Communication between two machines:</p>
<ul>
  <li>Ethernet frame: source mac + mac destiny + payload</li>
  <li>Ethernet is used to connect LAN device</li>
  <li>NIC: has unique MAC address (a hardware in a computer that provides an Ethernet port)</li>
  <li>Hub: connect devices but it is dumb. Send the frame to everyone. Open to colision</li>
  <li>Bridge: decide for who avoiding colision. </li>
  <li>Switch: hub + bridge. MAC table</li>
  <li>Unicast: one-to-one</li>
  <li>Routers break up broadcast segments </li>
  <li>ARP requests are L2 broadcasts: network message used to query a device's MAC address when its IP address is known</li>
  <li>Multicast: A destination MAC address is not recognized by the switch and is therefore sent out to all ports in the same VLAN except the source port, in order to discover the correct destination</li>
</ul>

<p>Layers</p>
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
    <td>physical characteristics for transmitting data > phisical address > connect to a cable > NIC, Ethernet, Hub, repeater > sends bits of data</td>
  </tr>
</table>
 
<p>Calculate the subnet (CIDR NOTATION) <a href="https://matt-rickard.com/how-to-calculate-a-cidr">[1]</a><a href="https://networkcalc.com/articles/cidr-notation/">[2]</a><a href="https://dev.to/rishitashaw/cidr-a-brief-overview-subnet-calculation-pfc">[3]</a></p>
<table>
  <tr>
    <td>
      10.1.1.0/24 > 10.1 is the subnet. 24 first bits are the network address (10.1.1 or 10.1.2) and the last one will be used for the IP address<br />
      10.1.0.0/16 means 10.1 or 10.2 is the network. So, can use 10.1.255.255 as IPs<br />
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


<p>VLAN avoid many physical switches. Logical segmentation. Each LAN has a subnet. VLANs are inside to swiche. Use router to communicate among the VLANs.</p>

<p>Router is connected to a switch on a trunk port. Trunk port is a network port on a switch that can carry traffic for multiple VLANs.</p>

<p>WAN: Wide Area Networks. Connect router of different and distant network. Router use WAN interface
Router send message to neibors or sent to internet (0.0.0.0/0 -> data centers).</p>

<p>IPSEC VPN. Router configure VPN. Public IP using securely tunnel using secrets.</p>

<p>Redundancy. Multiple router. SPOF  - single point of failure.</p>

<p>DHCP: Dynamic Host Protocol. When a machine issues a DHCP (Dynamic Host Configuration Protocol) request, it typically sends an Ethernet broadcast message on the local network. This broadcast is used to discover and contact a DHCP server within the network, requesting an IP address assignment and other network configuration information. (Layer 2 - Ethernet broadcast is sent).</p>

<p>DNS: Domain Name System (nslookup www.google.com -> DNS query to find the IP address)<a href="https://www.youtube.com/watch?v=QTu7yDnR_58&list=PLTk5ZYSbd9MhMmOiPhfRJNW7bhxHo4q-K&index=2">[4]</a></p>

<p>NAT (Network Address Translation) is a networking technique that modifies network address information in data packets as they pass through a router or firewall, allowing multiple devices within a local network to share a single public IP address for communication with external networks like the internet. This process helps conserve public IP addresses and adds a layer of security by hiding internal network structures from external sources.</p>

<p>NTP: Network Time Protocol <a href="https://www.meridianoutpost.com/resources/articles/IP-classes.php">[5]</a></p>


<p>Variable Length Subnet Masking (VLSM): the primary puerpose if to allocate IP address more efficiently by allowing for different subnet sizes within the same network.</p>


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


