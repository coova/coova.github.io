---
layout: page
title: CoovaChilli - chilli_radconfig(1)
permalink: /CoovaChilli/chilli_radconfig(1).html
---

NAME
-----------------------------------------

chilli_radconfig -  Utility function to fetch configurations over RADIUS 

SYNOPSIS
-----------------------------------------

***chilli_radconfig*** [ *chilli options* ] 

DESCRIPTION
-----------------------------------------

***chilli_radconfig*** is a simple utility to fetch ***chilli*** configurations from a central server using RADIUS. It takes the same arguments as ***chilli*** (so that it can run off the same configuration file), but only looks for a small number of settings to perform an *Administrative-User* login. The utility will print out the value of all the *ChilliSpot-Config* attributes in the Access-Accept. 

EXAMPLES
-----------------------------------------

 *# chilli_radconfig --radiusserver1=192.168.1.1 * \
 --radiussecret=MySecret --adminuser=chillispot  \
 --adminpasswd=chillispot > hs.conf 

SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) [chilli.conf](/CoovaChilli/chilli.conf(5).html) [chilli-radius](/CoovaChilli/chilli-radius(5).html) 

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. The original ChilliSpot project homepage is/was at www.chillispot.org. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
