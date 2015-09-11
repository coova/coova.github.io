---
layout: page
title: CoovaChilli - chilli(8)
permalink: /CoovaChilli/chilli(8).html
---

NAME
-----------------------------------------

chilli -  A Software Access Controller for Captive Portal and WPA 

SYNOPSIS
-----------------------------------------

***chilli*** --help 

***chilli*** --version 

***chilli*** [ *configuration options* ] 

***chilli*** -fd [ *configuration options* ] # for debugging in foreground 

DESCRIPTION
-----------------------------------------

***chilli*** is a software access controller typically used in Wireless LAN HotSpot. It supports of two different access methods for a Wireless LAN HotSpot: Universal Access Method (UAM) as well as Wireless Protected Access (WPA). This version of ***chilli*** is called CoovaChilli, a fork of the original ChilliSpot. See *http://www.coova.org/* for more information. 

***chilli*** has three major interfaces: A downlink interface for accepting connections from clients, a radius interface for authenticating clients and an uplink network interface for forwarding traffic to other networks. 

Authentication of clients is performed by an external radius server. For UAM the CHAP-Challenge and CHAP-Password as specified by RFC 2865 is used. For WPA the radius EAP-Message attribute as defined in RFC 2869 is used. The message attributes described in RFC 2548 are used for transferring encryption keys from the radius server to chilli. Furthermore the radius interface supports accounting. 

The downlink interface accepts DHCP and ARP requests from clients. The client can be in two states: Unauthenticated and authenticated. In unauthenticated state, web requests from the client are redirected to an authentication web server - the captive portal. 

In a typical application unauthenticated clients will be forwarded to a web server and prompted for username and password. The web server forwards the user credentials to ***chilli*** by means of web browser redirects. On the ***chilli*** side, authentication requests are forwarded to a radius server. If authentication is successful the state of the client is changed to authenticated. This authentication method is known as Universal Access Method (UAM). 

As an alternative to UAM, the access points can be configured to authenticate the clients by using Wireless Protected Access (WPA). In this case, authentication credentials are forwarded from the WPA access point to ***chilli*** by using the radius protocol. The received radius request is proxied by ***chilli*** and forwarded to the radius server. 

The uplink interface is implemented by using the ***TUN/TAP driver.*** When ***chilli*** is started, a tun interface is established and an optional external configuration script is called. 

Runtime errors are reported using the ***syslogd (8)*** facility. 

OPTIONS
-----------------------------------------

Configuration parameters set on the command line always take precedent over anything configured in a file. See [chilli.conf](/CoovaChilli/chilli.conf(5).html) for a complete list of possible configurations. Here are just a few common command line options: 

> ***--help*** 

Print help and exit. 

> ***--version*** 

Print version and exit. 

> ***--fg*** 

Run in foreground (default = off) 

> ***--debug*** 

Run in debug mode (default = off) 

> ***--conf*** *file* 

Configuration file to use instead of the default below. See [chilli.conf](/CoovaChilli/chilli.conf(5).html) for more inforamtion. 

> ***--pidfile*** *file* 

File to put the process ID instead of the default below. 

> ***--cmdsock*** *file* 

UNIX socket file for inter-process communication instead of default below. 

> ***--statedir*** *path* 

Directory of nonvolatile data instead of default below. 

FILES
-----------------------------------------

*/usr/local/etc/chilli.conf* 
>The main ***chilli*** configuration file. 

*/usr/local/etc/chilli/defaults* 
>Default configurations used by the ***chilli*** init.d and ***functions*** scripts. 

*/usr/local/etc/chilli/config* 
>Location specific configurations used by ***chilli*** init.d and ***functions*** scripts. Copy the ***defaults*** file mentioned above and edit. 

*/usr/local/etc/chilli/functions* 
>Helps configure ***chilli*** by loading the above configurations, sets some defaults, and provides functions for writing ***main.conf, hs.conf,*** and ***local.conf*** based on local and possibily centralized. See [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

*/usr/local/etc/init.d/chilli* 
>The init.d file for ***chilli*** which defaults to using the above configurations to build a set of configurations files in the /usr/local/etc/chilli directory - taking local configurations and optionally centralized configurations from RADIUS or a URL. See [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

*/usr/local/var/run/chilli.sock* 
>UNIX socket used to daemon communication. See [chilli_query](/CoovaChilli/chilli_query(1).html) 

*/usr/local/var/run/chilli.pid* 
>Process ID file. 

*/usr/local/etc/chilli/www/* 
>The typical directory for embedded web content served up by ***chilli*** using a minimal web server. A convenient place for the splash page, embedded captive portal, and JSON javascript resources. 


SIGNALS
-----------------------------------------

Sending HUP to chilli will cause the configuration file to be reread and DNS lookups to be performed. The configuration options are not affected by sending HUP: ***fg***, ***conf***, ***pidfile***, ***statedir***, ***net***, ***dynip***, ***statip***, ***uamlisten***, ***uamport***, ***radiuslisten***, ***coaport***, ***coanoipcheck***, ***proxylisten***, ***proxyport***, ***proxyclient***, ***proxysecret***, ***dhcpif***, ***dhcpmac***, ***lease***, or ***eapolenable*** 

The above configuration options can only be changed by restarting the daemon. 

SEE ALSO
-----------------------------------------

[chilli.conf](/CoovaChilli/chilli.conf(5).html) [chilli-radius](/CoovaChilli/chilli-radius(5).html) [chilli_opt](/CoovaChilli/chilli_opt(1).html) [chilli_query](/CoovaChilli/chilli_query(1).html) [chilli_radconfig](/CoovaChilli/chilli_radconfig(1).html) [chilli_response](/CoovaChilli/chilli_response(1).html) ***syslogd(8)***

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. The original ChilliSpot project homepage is/was at www.chillispot.org. 

Besides the long options documented in this man page ***chilli*** also accepts a number of short options with the same functionality. Use ***chilli --help*** for a full list of all the available options. 

The ***TUN/TAP driver is required*** for proper operation of the ***chilli*** server. Linux kernels later than 2.4.7 already include the driver, but typically needs to be loaded manually with ***modprobe tun*** or automaticly by adding ***alias char-major-10-200 tun*** to the ***/etc/modules.conf*** configuration file. For other platforms see *http://vtun.sourceforge.net/tun/* for information on how to install and configure the TUN/TAP driver. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2002-2005 by Mondru AB., 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
