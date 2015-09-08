---
status: old
layout: post
title: DHCP Discovery
created: 1201263278
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
The <a href="http://www.ietf.org/rfc/rfc2131.txt">Dynamic Host Configuration Protocol</a> (DHCP) is a standard way for client devices to acquire an IP address and other configurations (DNS, Gateway, etc) on a network. This is particularly true in public access networks; as such, DHCP is integral to chilli, and always has been. Of course, it could certainly be more flexible. As it is now, you can't really do much in the way of customizing your DHCP configurations. I have some ideas for <a href="/CoovaChilli">CoovaChilli</a>, and some DHCP discovery to share.

<strong>DHCP and MAC Authentication</strong>

MAC authentication is a common feature to access controllers that perform DHCP. It allows for authentication to take place automatically without the need of a captive portal or a web browser. CoovaChilli (and ChilliSpot) has the option to authenticate MAC addresses. Using this feature, initial DHCP requests made by the client trigger a RADIUS <tt>Access-Request</tt>. Subsequent DHCP requests from the client are granted with an authentication state based on the RADIUS response being <tt>Access-Accept</tt> or <tt>Access-Reject</tt>. That will change with the <em>macauthdeny</em> option, to have <tt>Access-Reject</tt> mean complete <a href="http://en.wikipedia.org/wiki/Blacklist">black-listing</a>, but more could be done.

Here are the DHCP options found in a request from a Windows XP laptop (the Parameter Request List being the same in DHCP Discover messages):
<pre>Option&nbsp;53:&nbsp;DHCP&nbsp;Message&nbsp;Type&nbsp;=&nbsp;DHCP&nbsp;Request
Option&nbsp;61:&nbsp;Client&nbsp;identifier
&nbsp;&nbsp;&nbsp;&nbsp;Hardware&nbsp;type:&nbsp;Ethernet
&nbsp;&nbsp;&nbsp;&nbsp;Client&nbsp;MAC&nbsp;address:&nbsp;00:18:xx:xx:xx:xx&nbsp;(00:18:xx:xx:xx:xx)
Option&nbsp;12:&nbsp;Host&nbsp;Name&nbsp;=&nbsp;"laptop"
Option&nbsp;81:&nbsp;FQDN
&nbsp;&nbsp;&nbsp;&nbsp;Flags:&nbsp;0x00
&nbsp;&nbsp;&nbsp;&nbsp;A-RR&nbsp;result:&nbsp;0
&nbsp;&nbsp;&nbsp;&nbsp;PTR-RR&nbsp;result:&nbsp;0
&nbsp;&nbsp;&nbsp;&nbsp;Client&nbsp;name:&nbsp;laptop.coova.org
Option&nbsp;60:&nbsp;Vendor&nbsp;class&nbsp;identifier&nbsp;=&nbsp;"MSFT&nbsp;5.0"
Option&nbsp;55:&nbsp;Parameter&nbsp;Request&nbsp;List
&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;=&nbsp;Subnet&nbsp;Mask
&nbsp;&nbsp;&nbsp;&nbsp;15&nbsp;=&nbsp;Domain&nbsp;Name
&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;=&nbsp;Router
&nbsp;&nbsp;&nbsp;&nbsp;6&nbsp;=&nbsp;Domain&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;44&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;46&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Node&nbsp;Type
&nbsp;&nbsp;&nbsp;&nbsp;47&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Scope
&nbsp;&nbsp;&nbsp;&nbsp;31&nbsp;=&nbsp;Perform&nbsp;Router&nbsp;Discover
&nbsp;&nbsp;&nbsp;&nbsp;33&nbsp;=&nbsp;Static&nbsp;Route
&nbsp;&nbsp;&nbsp;&nbsp;249&nbsp;=&nbsp;Classless&nbsp;static&nbsp;routes
&nbsp;&nbsp;&nbsp;&nbsp;43&nbsp;=&nbsp;Vendor-Specific&nbsp;Information
End&nbsp;Option</pre>
The following <a href="http://dev.coova.org/svn/coova-chilli/doc/dictionary.chillispot">Vendor Specific Attributes</a> (VSA) are proposed additions to <a href="/CoovaChilli">CoovaChilli</a> in order to forward this information to the RADIUS server during MAC authentication:
<pre>DHCP&nbsp;Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RADIUS&nbsp;Attribute
--------------------------------&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--------------------------------&nbsp;&nbsp;&nbsp;&nbsp;
Option&nbsp;12:&nbsp;Host&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChilliSpot-DHCP-Hostname
Option&nbsp;55:&nbsp;Parameter&nbsp;Request&nbsp;List&nbsp;&nbsp;&nbsp;&nbsp;ChilliSpot-DHCP-Parameter-Request-List
Option&nbsp;60:&nbsp;Vendor&nbsp;class&nbsp;identifier&nbsp;&nbsp;&nbsp;ChilliSpot-DHCP-Vendor-Class-Id
Option&nbsp;61:&nbsp;Client&nbsp;identifier&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChilliSpot-DHCP-Client-Id
Option&nbsp;81:&nbsp;FQDN&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChilliSpot-DHCP-Client-FQDN</pre>
Additionally, the VSA named <tt>ChilliSpot-DHCP-Options</tt> will be optional in either an <tt>Access-Accept</tt> or <tt>Access-Reject</tt>, carrying arbitrary options to append to the DHCP response. All attributes are binary octet strings and carry the DHCP options in raw form.

[img_assist|nid=206|title=|desc=|link=none|align=center|width=585|height=257]

Attributes in the <tt>Access-Request</tt> contain the corresponding DHCP option value, whereas the <tt>ChilliSpot-DHCP-Options</tt> contains a list of options, packed as they are in a DHCP message. Combined with the existing support for the <tt>Framed-IP-Address</tt> RADIUS attribute for IP assignment, this method provides for a high level of DHCP configuration centralized in your RADIUS server.

<strong>DHCP Relay Gateway</strong>

As the MAC authentication feature has shown, there is no reason why chilli can't delegate IP assignment. Then why not have chilli act as a DHCP forwarding agent? This would make it possible to centrally manage your DHCP configurations, using a more configurable server. <a href="/CoovaChilli">CoovaChilli</a> will be able to forward DHCP requests to a remote DHCP gateway, noting the IP assignment in the response.

[img_assist|nid=207|title=|desc=|link=none|align=center|width=525|height=214]

This would open up many possibilities... including, perhaps, captive portal settings provisioned through a DHCP server!

Note: You can already use <a href="/CoovaChilli">CoovaChilli</a> with access points, like the Cisco Aironet, configured to forward DHCP <em>to</em> chilli.

<strong>WPAD and Proxy Autoconfigure</strong>

Windows has a feature (in <em>Internet Options</em>, <em>Connections</em> tab, <em>LAN settings</em> button, <em>Automatically detect settings</em> checkbox) whereby browser proxy configurations can be picked up automatically from a network. <a href="http://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol">The Web Proxy Auto Discovery</a> (<a href="http://www.wpad.com/">WPAD</a>) protocol provides browsers (primarily Windows <a href="http://perimetergrid.com/wp/2008/01/11/wpad-internet-explorers-worst-feature/">Internet Explorer</a>, and <a href="http://www1.ietf.org/mail-archive/web/dhcwg/current/msg08227.html">maybe others</a>) with a proxy configuration file. This <a href="http://en.wikipedia.org/wiki/Proxy_auto-config">Proxy Auto-Config</a> (PAC) file can configure the default proxy and can be scripted, as demonstrated <a href="http://ap.coova.org/wpad.dat">in this example</a>, as a <a href="http://www.schooner.com/~loverso/no-ads/">banner ad buster</a>. Not without <a href="http://www.jcxp.net/news.php?newsid=2207">some risks</a>, the configuration is downloaded either based on a DHCP option or a DNS based web server (using the prefix "wpad." and the system FQDN).

With <em>Automatically detect settings</em> enabled, you will also see the following requests:
<pre>Option&nbsp;53:&nbsp;DHCP&nbsp;Message&nbsp;Type&nbsp;=&nbsp;DHCP&nbsp;Inform
Option&nbsp;61:&nbsp;Client&nbsp;identifier
&nbsp;&nbsp;&nbsp;&nbsp;Hardware&nbsp;type:&nbsp;Ethernet
&nbsp;&nbsp;&nbsp;&nbsp;Client&nbsp;MAC&nbsp;address:&nbsp;00:18:xx:xx:xx:xx&nbsp;(00:xx:xx:xx:xx:xx)
Option&nbsp;12:&nbsp;Host&nbsp;Name&nbsp;=&nbsp;"laptop"
Option&nbsp;60:&nbsp;Vendor&nbsp;class&nbsp;identifier&nbsp;=&nbsp;"MSFT&nbsp;5.0"
Option&nbsp;55:&nbsp;Parameter&nbsp;Request&nbsp;List
&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;=&nbsp;Subnet&nbsp;Mask
&nbsp;&nbsp;&nbsp;&nbsp;15&nbsp;=&nbsp;Domain&nbsp;Name
&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;=&nbsp;Router
&nbsp;&nbsp;&nbsp;&nbsp;6&nbsp;=&nbsp;Domain&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;44&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;46&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Node&nbsp;Type
&nbsp;&nbsp;&nbsp;&nbsp;47&nbsp;=&nbsp;NetBIOS&nbsp;over&nbsp;TCP/IP&nbsp;Scope
&nbsp;&nbsp;&nbsp;&nbsp;31&nbsp;=&nbsp;Perform&nbsp;Router&nbsp;Discover
&nbsp;&nbsp;&nbsp;&nbsp;33&nbsp;=&nbsp;Static&nbsp;Route
&nbsp;&nbsp;&nbsp;&nbsp;249&nbsp;=&nbsp;Classless&nbsp;static&nbsp;routes
&nbsp;&nbsp;&nbsp;&nbsp;43&nbsp;=&nbsp;Vendor-Specific&nbsp;Information
&nbsp;&nbsp;&nbsp;&nbsp;252&nbsp;=&nbsp;Proxy&nbsp;autodiscovery
End&nbsp;Option</pre>
Replying to either the DHCP Discover, Request, or Inform messages specifying the Proxy autodiscovery option will inform Windows of the required WPAD URL:
<pre>Option&nbsp;53:&nbsp;DHCP&nbsp;Message&nbsp;Type&nbsp;=&nbsp;DHCP&nbsp;ACK
Option&nbsp;1:&nbsp;Subnet&nbsp;Mask&nbsp;=&nbsp;255.0.0.0
Option&nbsp;3:&nbsp;Router&nbsp;=&nbsp;10.1.0.1
Option&nbsp;6:&nbsp;Domain&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;IP&nbsp;Address:&nbsp;208.67.222.222
&nbsp;&nbsp;&nbsp;&nbsp;IP&nbsp;Address:&nbsp;208.67.220.220
Option&nbsp;51:&nbsp;IP&nbsp;Address&nbsp;Lease&nbsp;Time&nbsp;=&nbsp;15&nbsp;minutes
Option&nbsp;54:&nbsp;Server&nbsp;Identifier&nbsp;=&nbsp;10.1.0.1
Option&nbsp;252:&nbsp;Proxy&nbsp;autodiscovery&nbsp;=&nbsp;"http://ap.coova.org/wpad.dat"
End&nbsp;Option</pre>
With the option specified, and since DHCP takes priority over any DNS based WPAD source, Internet Explorer happily takes the configuration. Even though my Mac sends the following in a DHCP Discover message:
<pre>Option&nbsp;53:&nbsp;DHCP&nbsp;Message&nbsp;Type&nbsp;=&nbsp;DHCP&nbsp;Discover
Option&nbsp;55:&nbsp;Parameter&nbsp;Request&nbsp;List
&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;=&nbsp;Subnet&nbsp;Mask
&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;=&nbsp;Router
&nbsp;&nbsp;&nbsp;&nbsp;6&nbsp;=&nbsp;Domain&nbsp;Name&nbsp;Server
&nbsp;&nbsp;&nbsp;&nbsp;15&nbsp;=&nbsp;Domain&nbsp;Name
&nbsp;&nbsp;&nbsp;&nbsp;112&nbsp;=&nbsp;NetInfo&nbsp;Parent&nbsp;Server&nbsp;Address
&nbsp;&nbsp;&nbsp;&nbsp;113&nbsp;=&nbsp;NetInfo&nbsp;Parent&nbsp;Server&nbsp;Tag
&nbsp;&nbsp;&nbsp;&nbsp;78&nbsp;=&nbsp;Directory&nbsp;Agent&nbsp;Information
&nbsp;&nbsp;&nbsp;&nbsp;79&nbsp;=&nbsp;Service&nbsp;Location&nbsp;Agent&nbsp;Scope
&nbsp;&nbsp;&nbsp;&nbsp;95&nbsp;=&nbsp;Lightweight&nbsp;Directory&nbsp;Access&nbsp;Protocol
&nbsp;&nbsp;&nbsp;&nbsp;252&nbsp;=&nbsp;Proxy&nbsp;autodiscovery
Option&nbsp;57:&nbsp;Maximum&nbsp;DHCP&nbsp;Message&nbsp;Size&nbsp;=&nbsp;1500
Option&nbsp;61:&nbsp;Client&nbsp;identifier&nbsp;(6&nbsp;bytes)
Option&nbsp;51:&nbsp;IP&nbsp;Address&nbsp;Lease&nbsp;Time&nbsp;=&nbsp;90&nbsp;days
Option&nbsp;12:&nbsp;Host&nbsp;Name&nbsp;=&nbsp;"iMac"
End&nbsp;Option</pre>
The Mac does not use the returned Proxy Autodiscovery option, at least not with Safari.

Still, interesting stuff... and could pose a problem if you are at a hotspot and your Windows laptop auto-configures a proxy server that is not accessible in the walled garden!
