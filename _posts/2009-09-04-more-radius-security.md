---
status: old
layout: post
title: More RADIUS Security
created: 1252061703
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
[RADIUS](http://tools.ietf.org/html/rfc2865) is a protocol "for carrying authentication, authorization, and configuration information between a Network Access Server (NAS) which desires to authenticate its links and a shared Authentication Server (AS)." RADIUS uses UDP packets that carry one or more RADIUS attributes.

There are several possible authentication protocols that can run within RADIUS. The simplest is PAP, where the user password is transmitted encoded with the shared secret between the NAS and AS. One of the more secure protocols is PEAP, used for secure networks requiring client software known as a *supplicant*, offers the same sort of mutual authentication and security as HTTPS/SSL. However, in all cases, the authentication protocol only serves to protect the user authentication credentials; there is no security for the other attributes which can include the user's username, their MAC address, and information about the NAS.

RADIUS over TLS
===============

[RadSec](http://tools.ietf.org/html/draft-ietf-radext-radsec-05) is a protocol that defines RADIUS over TLS. It provides a way to securely use RADIUS over the Internet without the need for more complicated VPN configurations.

RadSec in JRadius
================

[JRadius](/JRadius) now [supports RadSec](http://www.coova.org/JRadius/RadSec) both as a client and server. Other implementations include [Radiator](http://www.open.com.au/), a commercial RADIUS server, and [radsecproxy](http://software.uninett.no/radsecproxy/), a general purpose open-source RadSec/RADIUS proxy server.
