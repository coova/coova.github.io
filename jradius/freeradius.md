---
layout: page
title: JRadius - JRadius with FreeRADIUS
page_title: JRadius with FreeRADIUS
permalink: /JRadius/FreeRADIUS/
---

[JRadius](/JRadius) is not a stand-alone RADIUS server. Instead, it is a Java
Server which is called by the rlm_jradius module built into the FreeRADIUS
server. The module, using pooled connections to the JRadius server, passes the
RADIUS request and response packets to JRadius for any of the FreeRADIUS module
entry points. Meaning, you can have JRadius process authentication, accounting,
or proxy requests.

![JRadiusFreeRADIUS](/img/JRadiusFreeRADIUS.jpg)

The JRadius Server itself is a light-weight stand-alone Java server. Within its
XML configuration, JRadius can be configured with your specific
JRadius/FreeRADIUS Dictionary and any number of custom JRadius Handlers chained
together.

Building and Installing FreeRADIUS with JRadius
===============================================

The rlm_jradius module for FreeRADIUS is a standard module in the FreeRADIUS
distribution. However, it is not configured to be built per default. To build,
download the latest FreeRADIUS server:

    wget ftp://ftp.freeradius.org/pub/freeradius/freeradius-server-2.1.1.tar.bz2
    bzcat freeradius-server-2.1.1.tar.bz2 | tar xf -
    cd freeradius-server-2.1.1
    echo rlm_jradius >> src/modules/stable

Compile and install:

    ./configure
    make
    make install

Run FreeRADIUS (shown here in debug mode):

/usr/local/sbin/radiusd -X

Configuring for JRadius

Below are the portions of the FreeRADIUS etc/raddb/radiusd.conf file related to
JRadius. Also see the etc/raddb/ files in the patched distribution.

    modules {
       ...
       # configure the rlm_jradius module
       jradius {
          name      = "example"             # The "Requester" name (a single
                                            # JRadius server can have
                                            # multiple "applications")
          primary   = "localhost"           # Uses default port 1814
          secondary = "192.168.0.1"         # Fail-over server
          tertiary  = "192.168.0.1:8002"    # Fail-over server on port 8002
          timeout   = 1                     # Connect Timeout
          onfail    = NOOP                  # What to do if no JRadius
                                            # Server is found. Options are:
                                            # FAIL (default), OK, REJECT, NOOP
          keepalive = yes                   # Keep connections to JRadius pooled
          connections = 8                   # Number of pooled JRadius connections
      }
    }

In this example, the requester name is configured with name example. Different
requesters can be mapped to different handler chains in the JRadius context. You
can also configure primary, secondary, and tertiary JRadius servers for
redundancy fail-over. The TCP/IP connections to JRadius are pooled with
persistant connections if keepalive is yes.

    authorize {
       ...
       jradius
    }
 
    post-auth {
       ...
       jradius
       Post-Auth-Type REJECT {             # Use this to also process failures -
           jradius                         # AccessReject replies 
       }                                   # from the post-auth handler.
    }
  
    preacct {
       ...
       jradius
    }
  
    accounting {
       ...
       jradius
    }

You can put jradius in any of the FreeRADIUS stages, typically in authorize (to
among other things, add a user's plain text password in the FreeRADIUS context
for use in it's authenticate stage), post-auth, and accounting. It would be rare
to have jradius in the authenticate stage, since that is the part FreeRADIUS
does on its own. The above configurations are considered standard. But, if your
FreeRADIUS server is configured to proxy, then the following is also possible:

    pre-proxy {
       ...
       jradius
    }
  
    post-proxy {
       ...
       jradius
    }

[Run JRadius Server.](/JRadius/RunServer)
