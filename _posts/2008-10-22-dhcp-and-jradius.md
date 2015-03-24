---
layout: post
title: DHCP and JRadius
created: 1224663082
categories: []
---
The <a href="http://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol">Dynamic Host Configuration Protocol</a> (DHCP) is a protocol used by computers, or any network device, to automatically obtain an IP address and other related settings in order to access a network. Similar to RADIUS, DHCP is based on UDP requests and responses that can carry a wide range of attributes, or <em>options</em> as they are called in DHCP. Besides the typical options to assign IP Address, Default Router, and Domain Name Server, DHCP supports <a href="http://www.ietf.org/rfc/rfc2132.txt">many standard and vendor specific options</a> to configure devices on a network.

<strong>DHCP Support in FreeRADIUS</strong>

The latest <a href="http://freeradius.org/download.html">FreeRADIUS</a> server supports DHCP and JRadius, but not per default. <a href="http://www.coova.org/wiki/JRadius_FreeRADIUS">Build FreeRADIUS with JRadius support</a>, but also include DHCP by run the configure script with the <strong>&#45;&#45;with-dhcp</strong> option. Additionally, after installation edit the main dictionary file (/usr/local/share/freeradius/dictionary if the default installation prefix is used) to include <strong>$INCLUDE dictionary.dhcp</strong> - you will find the line already in the dictionary file, just commented out. Next, enable the DHCP service in FreeRADIUS by copying the file <strong>etc/raddb/sites-available/dhcp</strong> to the <strong>etc/raddb/sites-enabled/</strong> directory.

When FreeRADIUS received DHCP packets, it handles the packet very similarly to RADIUS packets - parsing the options into <a href="http://dev.coova.org/svn/cjradius/trunk/freeradius/dict/dictionary.dhcp">FreeRADIUS defined vendor specific attributes</a> and invoking modules. Thus allowing for DHCP programming in any one of the supported <a href="http://wiki.freeradius.org/Base_Modules">FreeRADIUS modules</a> (perl, python, sql, etc), including Java using the <a href="http://wiki.freeradius.org/Rlm_jradius">rlm_jradius</a> module.

<strong>DHCP Support in JRadius</strong>

In the etc/raddb/sites-enabled/dhcp configuration file, enable the jradius module to handle the various DHCP requests of interest.
<pre>server dhcp {
&nbsp;&nbsp;listen {
&nbsp;&nbsp;&nbsp;&nbsp;ipaddr = 127.0.0.1
&nbsp;&nbsp;&nbsp;&nbsp;port = 6700
&nbsp;&nbsp;&nbsp;&nbsp;type = dhcp
&nbsp;&nbsp;}
&nbsp;&nbsp;dhcp DHCP-Discover {
&nbsp;&nbsp;&nbsp;&nbsp;jradius
&nbsp;&nbsp;&nbsp;&nbsp;ok
&nbsp;&nbsp;}
&nbsp;&nbsp;dhcp DHCP-Request {
&nbsp;&nbsp;&nbsp;&nbsp;jradius
&nbsp;&nbsp;&nbsp;&nbsp;ok
&nbsp;&nbsp;}
&nbsp;&nbsp;dhcp DHCP-Decline {
&nbsp;&nbsp;&nbsp;&nbsp;jradius
&nbsp;&nbsp;&nbsp;&nbsp;ok
&nbsp;&nbsp;}
&nbsp;&nbsp;dhcp DHCP-Inform {
&nbsp;&nbsp;&nbsp;&nbsp;jradius
&nbsp;&nbsp;&nbsp;&nbsp;ok
&nbsp;&nbsp;}
}</pre>
The above configuration will run a DHCP server on the localhost port 6700 and will invoke JRadius for the specified DHCP packet types.

<strong>Example DHCP JRadius Handler</strong>

A <a href="http://dev.coova.org/svn/cjradius/trunk/extended/src/main/java/net/jradius/handler/dhcp/DHCPPoolHandler.java">simple DHCP IP Pool handler</a> is included, and pre-configured in the <a href="/JRadius/RunServer">JRadius example server</a>. The handler implements a simple IP address pool and takes care of all the DHCP logic. As you can see in the source code, it's just like a RADIUS handler just using the DHCP vendor specific attributes. Here is the debug output of a successful DHCP request and response as seen in JRadius after going through the handler:
<pre>Class: class net.jradius.packet.DHCPDiscover
Attributes:
DHCP-Opcode = Client-Message
DHCP-Hardware-Type = Ethernet
DHCP-Hardware-Address-Length = 6
DHCP-Hop-Count = 0
DHCP-Transaction-Id = 570983689
DHCP-Number-of-Seconds = 0
DHCP-Flags = Unknown-0
DHCP-Client-IP-Address = 0.0.0.0
DHCP-Your-IP-Address = 0.0.0.0
DHCP-Server-IP-Address = 0.0.0.0
DHCP-Gateway-IP-Address = 127.0.0.1
DHCP-Client-Hardware-Address = [Binary Data (length=6)]
DHCP-Message-Type = DHCP-Discover
DHCP-Parameter-Request-List = DHCP-Subnet-Mask
DHCP-Parameter-Request-List = DHCP-Router-Address
DHCP-Parameter-Request-List = DHCP-Domain-Name-Server
DHCP-Parameter-Request-List = DHCP-Domain-Name
DHCP-Parameter-Request-List = DHCP-Netinfo-Address
DHCP-Parameter-Request-List = DHCP-Netinfo-Tag
DHCP-Parameter-Request-List = DHCP-Directory-Agent
DHCP-Parameter-Request-List = DHCP-Service-Scope
DHCP-Parameter-Request-List = DHCP-LDAP
DHCP-Parameter-Request-List = Unknown-252
DHCP-DHCP-Maximum-Msg-Size = 1500
DHCP-Client-Identifier = [Binary Data (length=7)]
DHCP-IP-Address-Lease-Time = 7776000
DHCP-Hostname = laptop

Class: class net.jradius.packet.DHCPOffer
Attributes:
DHCP-Message-Type := DHCP-Offer
DHCP-Your-IP-Address := 10.1.0.74
DHCP-IP-Address-Lease-Time := 900
DHCP-DHCP-Server-Identifier := 10.1.0.1
DHCP-Domain-Name-Server := 10.1.0.1
DHCP-Subnet-Mask := 255.255.0.0
DHCP-Router-Address := 10.1.0.1</pre>

<strong>Example with CoovaChilli as Relay Agent</strong>

A DHCP server is built into CoovaChilli, but it can also be configured to relay DHCP requests to an external DHCP server. With CoovaChilli running on the same system as FreeRADIUS, the following configure is used for Chilli:
<pre>net 10.1.0.0/16
dynip 10.1.0.0/24
statip 10.1.1.0/24
uamlisten 10.1.0.1
radiusserver1 127.0.0.1
radiussecret testing123
dhcpif eth0
dns1 192.168.10.1
uamserver http://10.1.0.1/login.php
uamsecret uamsecret
uamanydns
dhcpradius
dhcpgateway 127.0.0.1
dhcpgatewayport 6700
dhcprelayagent 127.0.0.1</pre>
Where the last 3 options are the most relevant. Of course, your configuration will vary. Note that the DHCP relay and MAC authentication options are currently not playing well together, and that this is in general an experimental feature, as is DHCP support in FreeRADIUS and JRadius. Patches and bug reports are welcome in the <a href="/forum/">forum</a> and <a href="/MailingLists">mailing lists</a>.
