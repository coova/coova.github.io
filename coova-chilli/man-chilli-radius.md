---
layout: page
title: CoovaChilli - chilli-radius(5)
permalink: /CoovaChilli/chilli-radius(5).html
---

NAME
-----------------------------------------

chilli-radius -  Information about RADIUS in chilli 

DESCRIPTION
-----------------------------------------

***chilli*** uses RADIUS for access provisioning and statistics. Standards and best practices defined in RFCs are followed as best possible. However, ***chilli*** does take some liberties and bends the rules in places to better adapt to the more dynamic application of captive portals. 

See *http://www.coova.org/CoovaChilli/RADIUS* for details. 

ATTRIBUTES
-----------------------------------------

The RADIUS Attributes used by ***chilli*** and a short description: 

> ***User-name (1)*** 

Full username as entered by the user. 

> ***User-Password (2)*** 

Used for UAM as alternative to CHAP-Password and CHAP-Challenge. 

> ***CHAP-Password (3)*** 

Used for UAM CHAP Authentication 

> ***CHAP-Challenge (60)*** 

Used for UAM CHAP Authentication 

> ***EAP-Message (79)*** 

Used for WPA Authentication 

> ***NAS-IP-Address (4)*** 

IP address of Chilli (set by the ''nasip'' or ''radiuslisten'' option, and otherwise "0.0.0.0") 

> ***Service-Type (6)*** 

Set to Login (1) for normal authentication requests.  The Access-Accept message from the radius server for configuration management messages must also be set to Administrative-User. 

> ***Framed-IP-Address (8)*** 

IP address of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***Framed-IP-Netmask (9)*** 

IP netmask of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***Filter-ID (11)*** 

Filter ID pass on to scripts possibly. 

> ***Reply-Message (18)*** 

Reason of reject if present. 

> ***State (24)*** 

Sent to chilli in Access-Accept or Access-Challenge. Used transparently in subsequent Access-Request. 

> ***Class (25)*** 

Copied transparently by chilli from Access-Accept to Accounting-Request. 

> ***Session-Timeout (27)*** 

Logout once session timeout is reached (seconds) 

> ***Idle-Timeout (28)*** 

Logout once idle timeout is reached (seconds) 

> ***Called-Station-ID (30)*** 

Set to the ''nasmac'' option or the MAC address of chilli. 

> ***Calling-Station-ID (31)*** 

MAC address of client 

> ***NAS-Identifier (32)*** 

Set to radiusnasid option if present. 

> ***Acct-Status-Type (40)*** 

1=Start, 2=Stop, 3=Interim-Update 

> ***Acct-Input-Octets (42)*** 

Number of octets received from client. 

> ***Acct-Output-Octets (43)*** 

Number of octets transmitted to client. 

> ***Acct-Session-ID (44)*** 

Unique ID to link Access-Request and Accounting-Request messages. 

> ***Acct-Session-Time (46)*** 

Session duration in seconds. 

> ***Acct-Input-Packets (47)*** 

Number of packets received from client. 

> ***Acct-Output-Packets (48)*** 

Number of packets transmitted to client. 

> ***Acct-Terminate-Cause (49)*** 

1=User-Request, 2=Lost-Carrier, 4=Idle-Timeout, 5=Session-Timeout, 11=NAS-Reboot 

> ***Acct-Input-Gigawords (52)*** 

Number of times the Acct-Input-Octets counter has wrapped around. 

> ***Acct-Output-Gigawords (53)*** 

Number of times the Acct-Output-Octets counter has wrapped around. 

> ***NAS-Port-Type (61)*** 

19=Wireless-IEEE-802.11 

> ***Message-Authenticator (80)*** 

Is always included in Access-Request. If present in Access-Accept, Access-Challenge or Access-reject chilli will validate that the Message-Authenticator is correct. 

> ***Acct-Interim-Interval (85)*** 

If present in Access-Accept chilli will generate interim accounting records with the specified interval (seconds). 

> ***WISPr-Location-ID (14122, 1)*** 

Location ID is set to the radiuslocationid option if present. Should be in the format: isocc=<ISO_Country_Code>, cc=<E.164_Country_Code>, ac=<E.164_Area_Code>, network=<ssid/ZONE> 

> ***WISPr-Location-Name (14122, 2)*** 

Location Name is set to the radiuslocationname option if present. Should be in the format: <OPERATOR_NAME>,<LOCATION> 

> ***WISPr-Logoff-URL (14122, 3)*** 

Included in Access-Request to notify the operator of the log off URL. Defaults to "http://uamlisten:uamport/logoff". 

> ***WISPr-Redirection-URL (14122, 4)*** 

If present the client will be redirected to this URL once authenticated. This URL should include a link to WISPr-Logoff-URL in order to enable the client to log off. 

> ***WISPr-Bandwidth-Max-Up (14122, 7)*** 

Maximum transmit rate (b/s). Limits the bandwidth of the connection. Note that this attribute is specified in bits per second. 

> ***WISPr-Bandwidth-Max-Down (14122, 8)*** 

Maximum receive rate (b/s). Limits the bandwidth of the connection. Note that this attribute is specified in bits per second. 

> ***WISPr-Session-Terminate-Time (14122, 9)*** 

The time when the user should be disconnected in ISO 8601 format (YYYY-MM-DDThh:mm:ssTZD). If TZD is not specified local time is assumed. For example a disconnect on 18 December 2001 at 7:00 PM UTC would be specified as 2001-12-18T19:00:00+00:00. 

> ***ChilliSpot-Max-Input-Octets (14559, 1)*** 

Maximum number of octets the user is allowed to transmit. After this limit has been reached the user will be disconnected. 

> ***ChilliSpot-Max-Output-Octets (14559, 2)*** 

Maximum number of octets the user is allowed to receive. After this limit has been reached the user will be disconnected. 

> ***ChilliSpot-Max-Total-Octets (14559, 3)*** 

Maximum total octets the user is allowed to send or receive. After this limit has been reached the user will be disconnected. 

> ***ChilliSpot-Bandwidth-Max-Up (14559, 4)*** 

Maximum bandwidth up 

> ***ChilliSpot-Bandwidth-Max-Down (14559, 5)*** 

Maximum bandwidth down 

> ***ChilliSpot-Config (14559, 6)*** 

Configurations passed between chilli and back-end as name value pairs 

> ***ChilliSpot-Lang (14559, 7)*** 

Language selected in user interface 

> ***ChilliSpot-Version (14559, 8)*** 

Contains the version of the running CoovaChilli 

> ***ChilliSpot-DHCP-Netmask (14559, 61)*** 

DHCP IP netmask of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***ChilliSpot-DHCP-DNS1 (14559, 62)*** 

DHCP DNS1 of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***ChilliSpot-DHCP-DNS2 (14559, 63)*** 

DHCP DNS2 of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***ChilliSpot-DHCP-Gateway (14559, 64)*** 

DHCP Gateway of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***ChilliSpot-DHCP-Domain (14559, 65)*** 

DHCP Domain of the user, which is configurable during MAC authentication in the Access-Accept. 

> ***MS-MPPE-Send-Key (311,16)*** 

Used for WPA 

> ***MS-MPPE-Recv-Key (311,17)*** 

Used for WPA 

SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) [chilli.conf](/CoovaChilli/chilli.conf(5).html) [chilli_radconfig](/CoovaChilli/chilli_radconfig(1).html) 

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2006-2011 Coova Techcnologies, LLC, 

CoovaChilli is licensed under the GNU General Public License.
