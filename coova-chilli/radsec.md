---
layout: page
title: CoovaChilli RadSec
permalink: /CoovaChilli/RadSec/
---

When built with SSL support, chilli can support the tunneling of RADIUS over
TLS/SSL, otherwise known as RadSec.

Configuring for RadSec support requires the following arguments set:

> **sslkeyfile** *file*

File containing the private key in PEM format.

> **sslcertfile** *file*

File containing the X.509 certificate in PEM format.

> **sslcafile** *file*

File containing the CA certificate in PEM format.

> **radiussecret** *radsec*

Shared secret in RadSec tunnel should always be radsec (per RFC).

> **radsec**

Option to start the chilli_radsec daemon.

See also
--------

- [JRadius RadSec](/JRadius/RadSec)
- [radsecproxy](https://software.uninett.no/radsecproxy/)
