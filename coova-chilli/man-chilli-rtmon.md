---
layout: page
title: CoovaChilli - chilli_rtmon(1)
permalink: /CoovaChilli/chilli_rtmon(1).html
---

NAME
-----------------------------------------

chilli_rtmon -  Default Route Monitor for CoovaChilli 

SYNOPSIS
-----------------------------------------

***chilli_rtmon*** -file <update file> -pid <chilli pid> [-debug] 

DESCRIPTION
-----------------------------------------

***chilli_rtmon*** is a utility to detected changes in the default route, discover the next hop MAC address, and update a file with the chilli ***nexthop*** option. After updating the file, a SIGHUP signal is sent to the running ***chilli*** server to instruct it to reread the configuration. 

EXAMPLES
-----------------------------------------

# chilli_rtmon -debug 

# chilli_rtmon -file /tmp/nexthop.conf -pid <pid> 

SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) 

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
