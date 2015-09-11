---
layout: page
title: CoovaChilli - chilli_query(1)
permalink: /CoovaChilli/chilli_query(1).html
---

NAME
-----------------------------------------

chilli_query -  Interface into the chilli server 

SYNOPSIS
-----------------------------------------

***chilli_query*** [ -s <unix-socket> ] <command> [<parameters>...] 

DESCRIPTION
-----------------------------------------

***chilli_query*** is an interface into the running ***chilli*** server. It provides an administrator the ability to see who is logged in, to force a client to be logged out, or force a client to be authorized. 

Commands: 

> ***list*** 

To list all connected clients (subscribers) providing the MAC Address, IP Address, internal chilli state (dnat, pass, etc), the session id (used in Acct-Session-ID), authenticated status (1 authorized, 0 not), user-name used during login, duration / max duration, idle time / max idle time, input octets / max input octets, output octets / max output octets, max total octets, status of option swapoctets, bandwidth limitation information, and the original URL. 

> ***listip*** *<ip-address>* 

Same as ***list*** but for one IP address. 

> ***listmac*** *<mac-address>* 

Same as ***list*** but for one MAC address. 

> ***authorize*** *<parameters>* 

To explicity authorize a client, or change the session parameters of an already authorized client, by setting a series of session parameters. 

> ***listippool*** 

Show the internal IP pool state. 

> ***listgarden*** 

Show the internal walled garden state. 

> ***listradqueue*** 

Show the internal RADIUS queue state. 

> ***addgarden*** *[ ip <ip> | mac <mac> ] data <uamallow-resource>* 

Add to the dynamic walled garden. When used without the 'ip' or 'mac' option, the entry applies to the global garden. Otherwise, it is session specific only if configured with --enable-sessgarden. 

> ***remgarden*** *[ ip <ip> | mac <mac> ] data <uamallow-resource>* 

Remove from the dynamic walled garden. When used without the 'ip' or 'mac' option, the entry applies to the global garden. Otherwise, it is session specific only if configured with --enable-sessgarden. 

>*PARAMETERS* > ***ip*** *<ip-address>* 

Select the session to be authorized by the IP address using this option (may be used with the option below) 

> ***sessionid*** *<session-id>* 

Select the session to be authorized by the Session-ID (may be used with the above option) 

> ***username*** *<username>* 

Sets the username of the session. 

> ***sessiontimeout*** *<seconds>* 

Sets the max session time of the session. 

> ***idletimeout*** *<seconds>* 

Sets the max idle time of the session. 

> ***maxoctets*** *<number-of-bytes>* 

Sets the max data (input + output) limit of the session. 

> ***maxinputoctets*** *<number-of-bytes>* 

Sets the max input data limit of the session. 

> ***maxoutputoctets*** *<number-of-bytes>* 

Sets the max output data limit of the session. 

> ***maxbwup*** *<bandwidth>* 

Sets the max up bandwidth of the session. 

> ***maxbwdown*** *<bandwidth>* 

Sets the max down bandwidth of the session. 

> ***logout*** *<client-mac-address>* 

Logout and releases the DHCP lease of a client explicitly based on the MAC address (gotten from a list command). 

EXAMPLES
-----------------------------------------

# chilli_query list 00:0D:XX:XX:XX:XX 10.1.0.3 dnat 46c83f70000 0 - 0/0 0/0 http://url.com 

# chilli_query authorize ip 10.1.0.3 sessiontimeout 60 username me 

# chilli_query list 00:0D:XX:XX:XX:XX 10.1.0.3 pass 46c83f70000 1 me 2/0 2/0 http://url.com 

# chilli_query logout 00:0D:XX:XX:XX:XX 

# chilli_query list | awk (aq{ ($5 == 1) { print "User " i++ print " MAC:                    " $1 print " IP Address:             " $2 print " Session ID:             " $4 print " Username:               " $6 print " Duration / Max:         " $7 print " Idle / Max:             " $8 print " Input Octets / Max:     " $9 print " Output Octets / Max:    " $10 print " Max Total Octets:       " $11 print " Using swapoctets:       " $12 print " % / Max Up Bandwidth:   " $13 print " % / Max Down Bandwidth: " $14 print " Original URL:           " $15 } }(aq User 1 MAC:             00-11-XX-XX-XX-XX IP Address:      10.1.0.2 Session ID:      46fd423c00000001 User URL:        http://www.yahoo.com/ Duration / Max:  219/0 Idle / Max:      3/0 

FILES
-----------------------------------------

*/usr/local/var/run/chilli.sock* 
>UNIX socket used to daemon communication. 


SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. The original ChilliSpot project homepage is/was at www.chillispot.org. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
