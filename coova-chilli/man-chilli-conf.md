---
layout: page
title: CoovaChilli - chilli.conf(5)
permalink: /CoovaChilli/chilli.conf(5).html
---

NAME
-----------------------------------------

chilli.conf -  Chilli Configuration 

DESCRIPTION
-----------------------------------------

***chilli*** has many configuration parameters which can either be used on the command line or in a configuration file. When on the command line, options are prefixed with two dashes and may or may not have an equal sign, for instance, these are equivalent: 

*chilli --uamallowed www.coova.org --uamanydns* 

*chilli --uamallowed="www.coova.org" --uamanydns* 

Options that do not have arguments behave the same way, just without any equal sign or second argument. When in the configuration file, options must not have any dashes, but can still be used with or without the equal sign, as in: 

*uamallowed "www.coova.org"* 

*uamallowed=www.coova.org* 

*uamanydns* 

Options given on the command line take precedent over any options defined in a configuration file. The default main configuration file is */usr/local/etc/chilli.conf* which can be overridden using the ***--conf*** option (or just ***--c*** for short) on the command line. Configuration files may also include other configuration files as in: 

*include /path/to/chilli/configfile.conf* 

Blank lines and comment lines starting with ***'#'*** are also allowed in the configuration file. 

OPTIONS
-----------------------------------------

As mentioned above, all options below are able to be put on the command line (prefixed with '--') or in a configuration file. A few options, shown below with the leading dashes, are typically only used on the command line. 

> ***--help*** 

Or ***-h*** for short; prints help and exits (command line) 

> ***--version*** 

Or ***-V*** for short; prints version and exits (command line) 

> ***--fg*** 

Or ***-f*** for short; runs server in foreground (command line) 

> ***--debug*** 

Or ***-d*** for short; run server in debug mode (command line) 

> ***--debugfacility*** *level* 

Increase the debug level (command line) (should be named debuglevel) 

> ***--conf*** *file* 

Or ***-c*** *file* for short; use the configuration file *file* instead of the default show in ***FILES*** (command line) 

> ***logfacility*** *facility* 

The ***syslog(8)***facility to use for logging. 

> ***interval*** *seconds* 

Re-read configuration file and do DNS lookups every interval seconds. This has the same effect as sending the HUP signal. If ***interval*** is 0 (zero) this feature is disabled. 

> ***pidfile*** *file* 

Filename to put the process id, see ***FILES*** for default. 

> ***statedir*** *path* 

Directory of non-volatile data, see ***FILES*** for default. 

> ***cmdsock*** *file* 

UNIX socket used for communication with [chilli_query](/CoovaChilli/chilli_query(1).html) see ***FILES*** for default. 

> ***cmdsocketport*** *port* 

UNIX port used for communication with [chilli_query](/CoovaChilli/chilli_query(1).html) Only used when cmdsocket is not defined. Default port is 42424 

> ***net*** *net* 

Network address of the uplink interface (default = 192.168.182.0/24). The network address is set during initialisation when ***chilli*** establishes a tun device for the uplink interface. The network address is specified as either <address>/<netmask> (192.168.182.0/255.255.255.0) or <address>/<prefix> (192.168.182.0/24). 

> ***dynip*** *net* 

Dynamic IP address pool. Specifies a pool of dynamic IP addresses. If this option is omitted the network address specified by the ***net*** option is used for dynamic IP address allocation. See the ***net*** option for a description of the network address format. 

> ***statip*** *net* 

Static IP address pool. Specifies a pool of static IP addresses. With static address allocation the IP address of the client can be specified by the radius server. Static address allocation can be used for both MAC authentication and Wireless Protected Access. 

> ***dhcpgateway*** *ipaddress* 

IP address of a DHCP server (on the uplink network). If configured DHCP requests will be relayed to this server. 

> ***dhcpgatewayport*** *port* 

Port number to use when relaying requests to the DHCP server configured via fI dhcpgateway fR at. Defaults to 67. 

> ***dhcprelayagent*** *ipaddress* 

IP address to use when relaying DHCP requests to the DHCP gateway. 

> ***dns1*** *host* 

DNS Server 1. It is used to inform the client about the DNS address to use for host name resolution. If this option is not given the system primary DNS is used. 

> ***dns2*** *host* 

DNS Server 2. It is used to inform the client about the DNS address to use for host name resolution. If this option is not given the system secondary DNS is used. 

> ***domain*** *domain* 

Domain name. It is used to inform the client about the domain name to use for DNS lookups. 

> ***ipup*** *script* 

Script executed after the TUN/TAP network interface has been brought up. Executed with the following parameters: *<device-name> <ip-address> <net-mask>* and with environment variables: 
>> ***DEV=*** *<tun/tap-device-name>* 

The TUN/TAP device being brought up. 

> ***ADDR=*** *<tun/tap-device-ip>* 

The TUN/TAP device IP address being brought up. 

> ***MASK=*** *<tun/tap-device-mask>* 

The TUN/TAP device net mask being brought up. 

> ***NET=*** *<tun/tap-device-net>* 

The TUN/TAP device network being brought up. 

> ***DHCPIF=*** *<interface>* 

The ***dhcpif*** configured in [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

> ***UAMPORT=*** *<port-num>* 

The ***uamport*** configured in [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

> ***UAMUIPORT=*** *<port-num>* 

The ***uamuiport*** configured in [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

> ***ipdown*** *script* 

Script executed after the tun network interface has been taken down with the same arguments and environment variables as above. 

> ***conup*** *script* 

Script executed after a session is authorized.  Executed with the following environment variables (see source code for possibly more): 
>

> ***DEV=*** *<tun/tap-device>* 

The TUN/TAP device. 

> ***ADDR=*** *<chilli-ip>* 

IP Address of chilli, see the ***uamlisten*** option. 

> ***NET=*** *<chilli-net>* 

Network of chilli, see the ***net*** option. 

> ***MASK=*** *<chilli-net-mask>* 

Network mask of chilli, see the ***net*** options. 

> ***NAS_IP_ADDRESS=*** *<radiuslisten>* 

Is set to the ***radiuslisten*** value. 

> ***NAS_ID=*** *<nas-id>* 

The ***radiusnasid*** option. 

> ***WISPR_LOCATION_ID=*** *<location-id>* 

The ***radiuslocationid*** option. 

> ***WISPR_LOCATION_NAME=*** *<location-name>* 

The ***radiuslocationname*** option. 

> ***USER_NAME=*** *<username>* 

User-name used to login. 

> ***FRAMED_IP_ADDRESS=*** *<client-ip>* 

The client's IP Address. 

> ***CALLING_STATION_ID=*** *<client-mac>* 

The client's MAC Address. 

> ***CALLED_STATION_ID=*** *<chilli-mac>* 

The MAC address of the chilli interface. 

> ***FILTER_ID=*** *<filter>* 

A possible filter ID returned in RADIUS Filter-ID. 

> ***SESSION_TIMEOUT=*** *<seconds>* 

The max session time, as set by RADIUS Session-Timeout. 

> ***IDLE_TIMEOUT=*** *<seconds>* 

The max idle time, as set by RADIUS Idle-Timeout. 

> ***WISPR_BANDWIDTH_MAX_UP=*** *<bandwidth>* 

Max up stream bandwidth set by RADIUS WISPr-Bandwidth-Max-Up. 

> ***WISPR_BANDWIDTH_MAX_DOWN=*** *<bandwidth>* 

Max down stream bandwidth set by RADIUS WISPr-Bandwidth-Max-Down. 

> ***CHILLISPOT_MAX_INPUT_OCTETS=*** *<bytes>* 

Max input octets set by RADIUS ChilliSpot-Max-Input-Octets. 

> ***CHILLISPOT_MAX_OUTPUT_OCTETS=*** *<bytes>* 

Max output octets set by RADIUS ChilliSpot-Max-Output-Octets. 

> ***CHILLISPOT_MAX_TOTAL_OCTETS=*** *<bytes>* 

Max total octets set by RADIUS ChilliSpot-Max-Total-Octets. 

> ***condown*** *script* 

Script executed after a session has moved from authorized state to unauthorized with the same environment variables as above. 

> ***ssid*** *ssid* 

A parameter that is passed on to the UAM server in the initial redirect URL. 

> ***vlan*** *vlan* 

A parameter that is passed on to the UAM server in the initial redirect URL. 

> ***nasip*** *ipaddress* 

Value to use in RADIUS NAS-IP-Address attribute. If not present, ***radiuslisten*** is used (which defaults to "0.0.0.0"). 

> ***nasmac*** *mac* 

MAC address value to use in RADIUS Called-Station-ID attribute. If not present, the MAC address of the ***dhcpif*** is used for Called-Station-ID. 

> ***radiuslisten*** *host* 

Local interface IP address to use for the radius interface. Defaults to the value used in RADIUS NAS-IP-Address when ***nasip*** is not set. 

> ***radiusserver1*** *host* 

The IP address of radius server 1 (default=rad01.coova.org). 

> ***radiusserver2*** *host* 

The IP address of radius server 2 (default=rad01.coova.org). 

> ***radiusauthport*** *port* 

The UDP port number to use for radius authentication requests (default 1812). 

> ***radiusacctport*** *port* 

The UDP port number to use for radius accounting requests (default 1813). 

> ***radiussecret*** *secret* 

Radius shared secret for both servers (default coova-anonymous). This secret should be changed in order not to compromise security. 

> ***radiusnasid*** *id* 

Network access server identifier (default nas01). 

> ***radiuslocationid*** *id* 

WISPr Location ID. Should be in the format: isocc=<ISO_Country_Code>, cc=<E.164_Country_Code>, ac=<E.164_Area_Code>, network=<ssid/ZONE>. This parameter is further described in the document: Wi-Fi Alliance - Wireless ISP Roaming - Best Current Practices v1, Feb 2003. 

> ***radiuslocationname*** *name* 

WISPr Location Name. Should be in the format: <HOTSPOT_OPERATOR_NAME>,<LOCATION>. This parameter is further described in the document: Wi-Fi Alliance - Wireless ISP Roaming - Best Current Practices v1, Feb 2003. 

> ***radiusnasporttype*** *type* 

Value of NAS-Port-Type attribute. Defaults to 19 (Wireless-IEEE-802.11). 

> ***radiusoriginalurl*** 

Flag (defaults to off) to send the ChilliSpot-OriginalURL RADIUS VSA in Access-Request. 

> ***adminuser*** *username* 

User-name to use for Administrative-User authentication in order to pick up chilli configurations and establish a device 'system' session. 

> ***adminpasswd*** *password* 

Password to use for Administrative-User authentication in order to pick up chilli configurations and establish a device 'system' session. 

> ***adminupdatefile*** *filename* 

The file to use as the Administrative-User update file. When used in combination with the above adminuser and adminpasswd options, ChilliSpot-Config RADIUS attributes found in the Administrative-User Access-Accept are put into the specified file. If the file changes, chilli will reload it's configuration (it's assumed that this file is included into the chilli configuration file). 

> ***swapoctets*** 

Swap the meaning of "input octets" and "output octets" as it related to RADIUS attribtues. 

> ***openidauth*** 

Allows OpenID authentication by sending *ChilliSpot-Config=allow-openidauth* in RADIUS Access-Requests to inform the RADIUS server of the option. 

> ***wpaguests*** 

Allows WPA Guest authentication by sending *ChilliSpot-Config=allow-wpa-guests* in RADIUS Access-Requests to inform the RADIUS server of the option. The RADIUS may return with an Access-Accept containing *ChilliSpot-Config=require-uam-auth* to give WPA access, but enforce the captive portal. 

> ***coaport*** *port* 

UDP port to listen to for accepting radius disconnect requests. 

> ***coanoipcheck*** 

If this option is given no check is performed on the source IP address of radius disconnect requests. Otherwise it is checked that radius disconnect requests originate from ***radiusserver1*** or ***radiusserver2.*** 

> ***proxylisten*** *host* 

Local interface IP address to use for accepting radius requests. 

> ***proxyport*** *port* 

UDP Port to listen to for accepting radius requests. 

> ***proxyclient*** *host* 

IP address from which radius requests are accepted. If omitted the server will not accept radius requests. 

> ***proxysecret*** *secret* 

Radius shared secret for clients. If not specified it defaults to ***radiussecret.*** 

> ***dhcpif*** *dev* 

Ethernet interface to listen to for the downlink interface. This option must be specified. 

> ***usetap*** 

Use the TAP interface instead of TUN (Linux only). 

> ***noarpentries*** 

Do not create arp table entries in when using TAP. (Linux only). 

> ***nexthop*** *mac-address* 

Specify a MAC address which is the layer 2 next hop to route packets to (used with ***usetap*** only). 

> ***rtmonfile*** *file* 

Option to launch the *chilli_rtmon* daemon with the specified file as the update file. The *chilli_rtmon* daemon will update the file with a ***nexthop*** ** configuration entry before sending *chilli* a SIGHUP to reread it's configuration. 

> ***tcpwin*** *number* 

Specify an integer value for the TCP Window and TCP Maximum Segment Size. If set, packets are rewritten with the values for both Window and MSS. 

> ***tundev*** *dev* 

The specific device to use for the TUN/TAP interface. 

> ***txqlen*** *bytes* 

The TX queue length to set on the TUN/TAP interface. 

> ***dhcpmac*** *address* 

MAC address to listen to. If not specified the MAC address of the interface will be used. The MAC address should be chosen so that it does not conflict with other addresses on the LAN. An address in the range 00:00:5E:00:02:00 - 00:00:5E:FF:FF:FF falls within the IANA range of addresses and is not allocated for other purposes. 
>The ***dhcpmac*** option can be used in conjunction with access filters in the access points, or with access points which supports packet forwarding to a specific MAC address. Thus it is possible at the MAC level to separate access point management traffic from user traffic for improved system security. 

The ***dhcpmac*** option will set the interface in promisc mode. 

> ***lease*** *seconds* 

Use a DHCP lease of seconds (default 600). 

> ***dhcpstart*** *number* 

Where to start assigning IP addresses (default 10). 

> ***dhcpend*** *number* 

Where to stop assigning IP addresses (default 254). 

> ***dhcpbroadcast*** 

Always respond to DHCP to the broadcast IP, when no relay. 

> ***eapolenable*** 

If this option is given IEEE 802.1x authentication is enabled. ChilliSpot will listen for EAP authentication requests on the interface specified by ***dhcpif.*** EAP messages received on this interface are forwarded to the radius server. 

> ***ieee8021q*** 

Option to enable support for 802.1Q/VLAN network on the ***dhcpif*** interface. 

> ***uamserver*** *url* 

URL of web server to use for authenticating clients. 

> ***uamhomepage*** *url* 

URL of homepage to redirect unauthenticated users to. If not specified this defaults to ***uamserver.*** 

> ***uamaaaurl*** *url* 

When chilli is built with the *--enable-chilliproxy* compile-time option, this configuration option can be used to define a URL to use for the HTTP AAA protocol described here: http://www.coova.org/CoovaChilli/Proxy 

> ***wisprlogin*** *url* 

A specific URL to be given in WISPr XML LoginURL. Otherwise, ***uamserver*** is used. 

> ***uamsecret*** *secret* 

Shared secret between uamserver and chilli. This secret should be set in order not to compromise security. 

> ***uamlisten*** *host* 

IP address to listen to for authentication of clients. If an unauthenticated client tries to access the Internet she will be redirected to this address. 

> ***uamport*** *port* 

TCP port to bind to for authenticating clients (default = 3990). If an unauthenticated client tries to access the Internet she will be redirected to this port on the ***uamlisten*** IP address. 

> ***uamuiport*** *port* 

TCP port to bind to for only serving embedded content. 

> ***uamallowed*** *domain* 

Comma separated list of resources the client can access without first authenticating. Each entry in the list can be a domain names, IP addresses, or network segment. Example: 

>***uamallowed*** *www.chillispot.org,10.11.12.0/24* 

Where each entry can be made more specific by specifying a protocol and port in the format *host/network:port* or *protocol:host/network* or *protocol:host/network:port* where *protocol* is a protocol name from /etc/protocols, *host/network* is just as above (a domain, IP, or network), and *port* is a port number. Example: 

***uamallowed*** *coova.org:80,icmp:coova.org* 

Adding to your walled garden is useful for allowing access to a credit card payment gateways, community website, or other publicly available resources. 

ChilliSpot resolves the domain names to a set of IP addresses during startup. Some big sites change the returned IP addresses for each lookup. This behaviour is not compatible with this option. Domain names in the list do get updated periodically based on the ***interval*** option. 

It is possible to specify the ***uamallowed*** option several times. This is useful if many domain names have to be specified. 

> ***uamdomain*** *domain* 

One domain prefix per use of the option; defines a list of domain names to automatically add to the walled garden. This is done by the inspecting of DNS packets being sent back to the subscriber. 

> ***uamregex*** *host-pattern::path-pattern::qs-pattern* 

When chilli is built with the ***--enable-chilliredir*** option given to the configure script, the ***uamregex*** option is available. The value should be a ***::*** separated list of three values; the regex patterns to match the Host header, the URL path, and the query string of the request. The patterns follow the ***regex(7)***syntax with the addition of ******* ** meaning anything (or to not check that field) and any pattern starting with ***!*** ** will be negated in meaning. 

Examples: 

*--uamregex='.google.com$::!^mail/::*'* 

This will allow all requests to a .google.com host except if the URL starts with mail (links to Gmail). 

> ***defsessiontimeout*** *seconds* 

Default session timeout (max session time) unless otherwise set by RADIUS (defaults to 0, meaning unlimited). 

> ***defidletimeout*** *seconds* 

Default idle timeout (max idle time) unless otherwise set by RADIUS (defaults to 0, meaning unlimited). 

> ***definteriminterval*** *seconds* 

Default interim-interval for RADIUS accounting unless otherwise set by RADIUS (defaults to 0, meaning unlimited). 

> ***defbandwidthmaxdown*** 

Default bandwidth max down set in bps, same as WISPr-Bandwidth-Max-Down. 

> ***defbandwidthmaxup*** 

Default bandwidth max up set in bps, same as WISPr-Bandwidth-Max-Up. 

> ***acctupdate*** 

Allow updating of session parameters with RADIUS attributes sent in Accounting-Response. 

> ***wwwdir*** *path* 

Directory where embedded local web content is placed. This content is accessible using the URL format http://<uamlisten>:<uamport>/www/<filename> 

> ***wwwbin*** *script* 

Executable to run as a CGI type program (like haserl) for URLs with extention ***.chi*** - in the format http://<uamlisten>:<uamport>/www/<file>.chi 

> ***uamui*** *script* 

An init.d style program to handle local content on the ***uamuiport*** web server. 

> ***uamanydns*** 

Allow any DNS server. Normally unauthenticated clients are only allowed to communicate with the DNS servers specified by the ***dns1*** and ***dns2*** options. If the ***uamanydns*** option is given ChilliSpot will allow the client to use all DNS servers. This is convenient for clients which are configured to use a fixed set of DNS servers. Since the server may not be available, requests are forwarded to the ***dns1*** server. 

> ***uamlogoutip*** *ipaddress* 

Use this IP address to instantly logout a client accessing it (defaults to 1.0.0.0). 

> ***uamaliasip*** *ipaddress* 

A special IP address that will always get hijacked to the UAM server (either to the uamuiport, if defined, otherwise uamport; defaults to 1.0.0.1). 

> ***uamaliasname*** *name* 

An (unqualified, so no dots) hostname that is used as a DNS alias for the ***uamaliasip*** defined above. Any DNS request for this hostname, or this hostname under the ***domain*** will be returned with the ***uamaliasip*** IP address. 

> ***dnsparanoia*** 

Inspect DNS packets and drop responses with any non- A, CNAME, SOA, or MX records (to prevent dns tunnels; experimental). 

> ***domaindnslocal*** 

Option to have chilli return the ***uamaliasip*** for all DNS requests for a hostname under the ***domain*** that is configured. 

> ***uamanyip*** 

Allow clients to use any IP settings they wish by spoofing ARP (experimental). 

> ***nouamsuccess*** 

Do not return to UAM server on login success, just redirect to original URL. 

> ***nouamwispr*** 

Do not do any WISPr XML, assume the back-end is doing this instead. 

> ***usestatusfile*** 

Write the status of clients in a non-volatile state file (experimental). 

> ***chillixml*** 

Return the so-called Chilli XML along with WISPr XML. 

> ***macauth*** 

If this option is given ChilliSpot will try to authenticate all users based on their mac address alone. The User-Name sent to the radius server will consist of the MAC address and an optional suffix which is specified by the ***macsuffix*** option. If the ***macauth*** option is specified the ***macallowed*** option is ignored. 

> ***macallowed*** *mac* 

List of MAC addresses for which MAC authentication will be performed. Example: 

>***macallowed*** *00-0A-5E-AC-BE-51,00-30-1B-3C-32-E9* 

The User-Name sent to the radius server will consist of the MAC address and an optional suffix which is specified by the ***macsuffix*** option. If the ***macauth*** option is specified the ***macallowed*** option is ignored. 

It is possible to specify the ***macallowed*** option several times. This is useful if many mac addresses has to be specified. 

> ***macsuffix*** *suffix* 

Suffix to add to the MAC address in order to form the User-Name, which is sent to the radius server. 

> ***macpasswd*** *password* 

Password used when performing MAC authentication. (default = password) 

> ***macallowlocal*** 

An option to allow MAC authentication based on ***macallowed*** without the use of RADIUS authentication. 

> ***ethers*** *file* 

A file containing MAC address and IP address mappings for DHCP allocation. The file should be formatted as: 

>00-XX-XX-XX-XX-XX  IP.IP.IP.IP 

> ***localusers*** *file* 

A colon seperated file containing usernames and passwords of locally authenticated users. 

> ***postauthproxy*** *ipaddress* 

Used with ***postauthproxyport*** to define a post authentication HTTP proxy server. 

> ***postauthproxyport*** *port* 

Used with ***postauthproxy*** to define a post authentication HTTP proxy server. 

> ***locationname*** *name* 

Human readable location name used in JSON interface. 

> ***papalwaysok*** 

(now depreciated; always on) Was used to allow PAP authentication. 

SSL OPTIONS
-----------------------------------------

The following options are available when chilli is built with SSL support. 

> ***sslkeyfile*** *filename* 

Defines the location of the PEM formatted private key file. 

> ***sslkeypass*** *password* 

The password (if any) that protects the private key. 

> ***sslcertfile*** *filename* 

Defines the location of the PEM formatted certificate file. 

> ***sslcafile*** *filename* 

Defines the location of the PEM formatted CA certificate file. 

> ***redirssl*** 

When set, HTTPS requests by unauthorized clients get hijacked instead of dropped. Requires at least ***sslkeyfile*** and ***sslcertfile*** to be defined. 

> ***uamuissl*** 

When set, the uamuiport is enabled with SSL. Requires at least ***sslkeyfile*** and ***sslcertfile*** to be defined. 

> ***radsec*** 

When set, a RadSec RADIUS tunnel is establised. Requires at least ***sslkeyfile***, ***sslcertfile***, and ***sslcafile*** to be defined. 

FILES
-----------------------------------------

*/usr/local/etc/chilli.conf* 
>The main ***chilli*** configuration file. Per default, this file includes three other files; ***main.conf, hs.conf,*** and ***local.conf.*** The main.conf and hs.conf are created by the shell script routines in ***functions*** based on configurations in the files mentioned below and possibility taking some configurations from a remote RADIUS server or URL. The local.conf file is reserved for location specific configurations. 

*/usr/local/etc/chilli/defaults* 
>Default configurations used by the ***chilli*** init.d and ***functions*** scripts in creating the actual configuration files. See the comments in this file for more information on how to configure ***chilli*** and related scripts and embedded content. 

*/usr/local/etc/chilli/config* 
>Location specific configurations used by ***chilli*** init.d and ***functions*** scripts. Copy the ***defaults*** file mentioned above and edit. This file is loaded after the ***defaults*** and thus will override settings. 

*/usr/local/etc/chilli/functions* 
>Helps configure ***chilli*** by loading the above configurations, sets some defaults, and provides functions for writing ***main.conf, hs.conf,*** and ***local.conf*** based on local and possibily centralized settings. 

*/usr/local/etc/init.d/chilli* 
>The init.d file for ***chilli*** which defaults to using the above configurations to build a set of configurations files in the /usr/local/etc/chilli directory - taking local configurations and optionally centralized configurations from RADIUS or a URL. 


SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) [chilli-radius](/CoovaChilli/chilli-radius(5).html) [chilli_opt](/CoovaChilli/chilli_opt(1).html) [chilli_radconfig](/CoovaChilli/chilli_radconfig(1).html) ***syslogd(8)***

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. The original ChilliSpot project homepage is/was at www.chillispot.org. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2002-2005 by Mondru AB., 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
