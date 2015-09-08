---
status: old
layout: post
title: RADIUS Secrets
created: 1273344297
categories:
- !binary |-
  dW5jYXRlZ29yaXplZA==
---
The importance of the RADIUS shared secret and security:

* Provides data integrity; meaning that you have confidence that the information received came from the trusted (by knowing the secret) source without modification.

* Protects the user password during PAP authentication. Knowing the RADIUS shared secret, the clear-text password can be derived from the PAP encoded password.

* Protects the RADIUS server from a variety of attacks by requiring all RADIUS data pass verification against the shared secret. Typically, this means the RADIUS server simply does not process the data, dropping the RADIUS requests.

* Select strong shared secrets. Use one for each client, as much as possible. It is also recommended to have all RADIUS protected in a secure tunnel such as a VPN or RadSec.

For more information on RADIUS security, here are a variety of links:

* [An Analysis of the RADIUS Authentication Protocol](http://www.untruth.org/~josh/security/radius/radius-auth.html)

* [Shared secrets: Internet Authentication Service (IAS)](http://technet.microsoft.com/en-us/library/cc740124%28WS.10%29.aspx)

* [Securing a RADIUS server](http://howto.techworld.com/mobile-wireless/3450/securing-a-radius-server/)

* [RADIUS Overview by HP](http://docs.hp.com/en/T1428-90026/ch01s01.html)

* [RadSec IETF Draft](http://tools.ietf.org/html/draft-ietf-radext-radsec-06)

* [JRadius / RadSec](http://www.coova.org/JRadius/RadSec)

* [CoovaChilli / RadSec](http://www.coova.org/CoovaChilli/RadSec)
