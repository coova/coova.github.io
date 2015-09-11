---
layout: page
title: CoovaChilli - chilli_opt(1)
permalink: /CoovaChilli/chilli_opt(1).html
---

NAME
-----------------------------------------

chilli_opt -  Configuration utility for CoovaChilli 

SYNOPSIS
-----------------------------------------

***chilli_opt*** <chilli-options> 

DESCRIPTION
-----------------------------------------

***chilli_opt*** is a utility to configure a ***chilli*** server. The utility take all the arguments of CoovaChilli, parses the configuration file, and then write out the configuration into a binary form ready for a running chilli server to pick up and use (without delay). 

This utilitiy is executed by ***chilli*** from a forked process to off-line the processing of the configuration, including waiting for any DNS resolution, etc. When ***chilli_opt*** is done processing the configuration, it writes it to a binary format (and system architecture depended) file. When executed by ***chilli*** the binary file used is *config.bin* found in a process specific directory in the temporary file system, such as */tmp/chilli-1000/config.bin* where 1000 is the process id of the running ***chilli*** server. 

EXAMPLES
-----------------------------------------

# chilli_opt --version 

# chilli_opt -b /tmp/chilli-[pid]/config.bin -r 

SEE ALSO
-----------------------------------------

[chilli](/CoovaChilli/chilli(8).html) [chilli.conf](/CoovaChilli/chilli.conf(5).html) 

NOTES
-----------------------------------------

See *http://www.coova.org/* for further documentation and community support. 

AUTHORS
-----------------------------------------

David Bird  

Copyright (C) 2006-2012 David Bird (Coova Technologies) All rights reserved. 

CoovaChilli is licensed under the GNU General Public License.
