---
status: old
status: old
layout: post
title: AP Location
created: 1274013940
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
- !binary |-
  YXBwbGljYXRpb25z
---
With <a href="/CoovaChilli">CoovaChilli</a> managing the traffic of multiple access points, it can now be configured to utilize the <i>MAC Authentication</i> features found in some WLAN products to learn the access point location of a subscriber device. To demonstrate the use of this feature, hear is an example using both the <a href="http://www.cisco.com/en/US/products/hw/wireless/ps430/index.html">Cisco Aironet</a> and the <a href="http://enterprise.alcatel-lucent.com/?product=WLANFamily&page=overview">Alcatel-Lucent/Aruba OmniAccess</a> switch.

CoovaChilli with AP/switch MAC Authentication
=============================================

![](/img/2010-05-16-ap-location/chilli-proxyvsa.png)

<b>(1)</b> The access point (or switch) performs a MAC authentication when the subscriber associates. CoovaChilli is configured to always reply with an <i>Access-Accept</i> after noting any Vendor Specific Attributes (VSAs) or the configured location attribute.

<b>(2)</b> Any VSAs plus <b>ChilliSpot-Location</b>, if a location attribute was specified, are sent in all RADIUS for the session.

<b>(3)</b> If the location attribute was specified, the <b>loc=attribute-value</b> query string parameter is sent to the captive portal in the initial redirect.

Cisco Aironet Example
=====================

The Cisco Aironet is able to provide multiple wireless networks and can put them on one or more VLAN networks. In this example, we configure the Cisco with one wireless signal configured with <i>MAC Authentication</i>. CoovaChilli is then setup to provide RADIUS services using it's <i>proxyport</i> (same port used for EAP/802.1x proxy) and to always reply with a RADIUS <i>Access-Accept</i> to MAC authentication requests. Additionally, CoovaChilli is configured to use the <i>NAS-Identifier</i> attribute sent by the Cisco as the location attribute.

<b>Configuring the Cisco Aironet 1200</b>

![](/img/2010-05-16-ap-location/cisco1.png)

Shown above is an overview of the Cisco configuration under the <b>Security</b> menu. In our case, we have a single wireless network with SSID <b>ap-cisco</b> that is configured with MAC authentication. We additionally have a RADIUS server defined, which is configured to use the CoovaChilli proxy settings.

Under <b>Server Manager</b>, we have a single RADIUS server using the CoovaChilli proxy configurations (listen IP, port, and secret).

![](/img/2010-05-16-ap-location/cisco2.png)

Under <b>SSID Manager</b>, we then have a wireless signal configured with <b>Open Authentication</b> <i>with MAC Authentication</i>.

![](/img/2010-05-16-ap-location/cisco3.png)

<b>CoovaChilli Configuration</b>

The RADIUS settings of the Cisco are that of the CoovaChilli proxy port. In this case, CoovaChilli will be listening on <i>10.1.1.1</i> port <i>1645</i> and with RADIUS shared secret <i>my-secret</i>. CoovaChilli is configured to get the location attribute <i>NAS-Identifier</i> (type 32) from the Cisco, and to respond with an <i>Access-Accept</i>.

/etc/chilli/eth1.100/config:

    HS_NASID=nas-100
    HS_NETWORK=10.100.1.0
    HS_NETMASK=255.255.255.0
    HS_UAMLISTEN=10.100.1.1
    HS_RADPROXY=on
    HS_RADPROXY_LISTEN=10.1.1.1
    HS_RADPROXY_CLIENT=10.1.1.0/24
    HS_RADPROXY_SECRET=my-secret
    HS_RADPROXY_PORT=1645
    HS_RADPROXY_MACACCEPT=on
    HS_RADPROXY_LOCATTR=32
    ...

<b>RADIUS MAC Authentication Access-Request from Cisco</b>

When a wireless client associates with the Cisco, it will do MAC authentication, sending information to CoovaChilli, which then responds with an <i>Access-Accept</i>.

    AccessRequest:
      User-Name (1) = 001124xxxxxx
      User-Password (2) = [String](Encrypted)
      Called-Station-Id (30) = 00-12-DA-XX-XX-XX
      Calling-Station-Id (31) = 00-11-24-XX-XX-XX
      Service-Type (6) = Login
      NAS-Port-Type (61) = Wireless - IEEE 802.11
      NAS-Port (5) = 264
      NAS-IP-Address (4) = 10.1.1.2
      NAS-Identifier (32) = ap-cisco

<b>RADIUS Access-Request from CoovaChilli</b>

After learning the location, CoovaChilli with then send the location information in all subsequent RADIUS for that session (MAC and UAM authentication) in the attribute <i>ChilliSpot-Location</i>.

    AccessRequest:
      ChilliSpot-Version = 1.2.3-rc1
      User-Name = 00-11-24-XX-XX-XX
      User-Password = [String](Encrypted)
      Calling-Station-Id = 00-11-24-XX-XX-XX
      Called-Station-Id = 00-06-4F-XX-XX-XX
      NAS-Port = 1
      NAS-IP-Address = 10.100.1.1
      Service-Type = Framed-User
      NAS-Identifier = nas-100
      Acct-Session-Id = 4bc5bf4a00000001
      NAS-Port-Type = Wireless-802.11
      WISPr-Location-ID = isocc=,cc=,ac=,network=MyHotspot,100
      WISPr-Location-Name = MyHotspot
      ChilliSpot-DHCP-Parameter-Request-List = [Data](Binary)
      ChilliSpot-DHCP-Client-Id = [Data](Binary)
      ChilliSpot-DHCP-Hostname = iMac
      ChilliSpot-Location = ap-cisco
      Message-Authenticator = [Data](Binary)

<b>Location in Initial Redirect</b>

The location is also present in the initial redirect URL query string, as:

<div style="line-height: 1; padding: 1em; border: 1px dashed grey; background-color: #eee"><code style="font-family: monospace;">...&amp;called=xx-xx-xx-xx-xx-xx&amp;nasid=nas-100&amp;<b>loc=ap-cisco</b>&amp;...</code>
</div>

<h3>Alcatel-Lucent OmniAccess Example</h3>

An example using the OmniAccess 4304 WLAN Switch from Alcatel-Lucent / Aruba.

For the <b>Network VLANs Configuration</b> we have a simple setup with physical port 8 is our WAN port, and is given IP address <i>10.1.1.2</i>. We then have a single VLAN setup on physical port 4, which has a subscriber network access point.

![](/img/2010-05-16-ap-location/omni0.png)

Under <b>Security / Authentication / Servers</b>, we have defined a single RADIUS server which points to our CoovaChilli RADIUS proxy port.

![](/img/2010-05-16-ap-location/omni1.png)

Under <b>Security / Authentication / Profiles</b>, ensure that the MAC Authentication profile is using <i>default</i>.

![](/img/2010-05-16-ap-location/omni2.png)

Under <b>Security / Authentication / L2 Authentication</b>, ensure that the MAC Authentication profiles has the <i>default</i> profile added.

![](/img/2010-05-16-ap-location/omni3.png)

Under <b>Security / Authentication / Advanced</b>, we configure the RADIUS client to be using the <i>10.1.1.2</i> IP address on the main interface.

![](/img/2010-05-16-ap-location/omni4.png)

For more information on how to setup your OmniAccess, please refer to your users manual.

<b>CoovaChilli Configuration</b>

The RADIUS settings used in the switch are that of the CoovaChilli proxy port. In this case, CoovaChilli will be listening on <i>10.1.1.1</i> port <i>1645</i> and with RADIUS shared secret <i>my-secret</i>. CoovaChilli is configured location attribute <i>Aruba-Location-Id</i> (vendor 14823, type 6), and to respond with an <i>Access-Accept</i>.

/etc/chilli/eth1.100/config:

    HS_NASID=nas-100
    HS_NETWORK=10.100.1.0
    HS_NETMASK=255.255.255.0
    HS_UAMLISTEN=10.100.1.1
    HS_RADPROXY=on
    HS_RADPROXY_LISTEN=10.1.1.1
    HS_RADPROXY_CLIENT=10.1.1.0/24
    HS_RADPROXY_SECRET=my-secret
    HS_RADPROXY_PORT=1645
    HS_RADPROXY_MACACCEPT=on
    HS_RADPROXY_LOCATTR="14823,6"
    ...

<b>RADIUS MAC Authentication Access-Request from OmniAccess</b>

When a subscriber associates to one of the access points, the switch sends CoovaChilli RADIUS similar to:

    AccessRequest:
      NAS-IP-Address = 10.1.1.2
      NAS-Port = 0
      NAS-Port-Type = Wireless-802.11
      User-Name = 001124XXXXXX
      User-Password = [String](Encrypted)
      Calling-Station-Id = 001302XXXXXX
      Called-Station-Id = 00064FXXXXXX
      Service-Type = Login
      Aruba-Essid-Name = ap-aruba
      Aruba-Location-Id = ap-aruba
      NAS-Identifier = nasname

The Vendor Specific Attributes (those starting with <i>Aruba-</i>) are then associated with the session and are used in CoovaChilli authentication.

<b>RADIUS Access-Request from CoovaChilli</b>

In our example, we also have chilli configured to use the <i>Aruba-Location-Id</i> as our <i>ChilliSpot-Location</i>. An example CoovaChilli MAC authentication after accepting the MAC authentication from the OmniAccess:

    AccessRequest:
      ChilliSpot-Version = 1.2.3-rc1
      User-Name = 00-11-24-XX-XX-XX
      User-Password = [String](Encrypted)
      Calling-Station-Id = 00-13-02-XX-XX-XX
      Called-Station-Id = 00-06-4F-XX-XX-XX
      NAS-Port = 1
      NAS-IP-Address = 10.100.1.1
      Service-Type = Framed-User
      NAS-Identifier = nas-100
      Acct-Session-Id = 4bc5bf4a00000001
      NAS-Port-Type = Wireless-802.11
      WISPr-Location-ID = isocc=,cc=,ac=,network=MyHotspot,100
      WISPr-Location-Name = MyHotspot
      ChilliSpot-DHCP-Parameter-Request-List = [Data](Binary)
      ChilliSpot-DHCP-Client-Id = [Data](Binary)
      ChilliSpot-DHCP-Hostname = iMac
      Aruba-Essid-Name = ap-aruba
      Aruba-Location-Id = ap-aruba
      ChilliSpot-Location = ap-aruba
      Message-Authenticator = [Data](Binary)

<b>Location in Initial Redirect</b>

Just like with the Cisco, the location is also sent in the initial redirect URL.

    ...&amp;called=xx-xx-xx-xx-xx-xx&amp;nasid=nas-100&amp;loc=ap-aruba&amp;...

This feature requires CoovaChilli 1.2.3.
