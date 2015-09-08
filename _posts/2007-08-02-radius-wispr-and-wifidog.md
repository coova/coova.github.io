---
status: old
layout: post
title: RADIUS, WISPr and WiFiDog
created: 1186050824
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
The <a href="http://dev.wifidog.org/">WiFiDog project</a> offers an excellent and highly customizable captive portal solution. Used by many free community networks and increasingly for commercial and pre-paid WiFi access providers, it offers an access controller application (in the access point) and a PHP based captive portal web application. Whereas <a href="/CoovaChilli">ChilliSpot</a>, also an access controller, does not offer much in the way of captive portal other than a generic perl CGI program. As an access controller, WiFiDog and ChilliSpot do similar functions. However, they differ in fundamental ways. For instance, Chilli relies on RADIUS in the access controller and does DHCP internally where WiFiDog requires it's accompanying captive portal application - RADIUS is done in PHP by the back-end - and does not control DHCP. WiFiDog uses iptables where Chilli does it's own packet switching. There are many differences as WiFiDog relies more on the web based back-end and Chilli focuses on RADIUS and features in the access controller.

Bringing some of the lesson learned with Chilli, some <a href="/WiFiDog/Patches">patches are now available</a> for testing to: improving RADIUS support, add WISPr XML, and introduce MAC Authentication to the WiFiDog suite.

<strong>RADIUS improvements</strong> include the use of Called/Calling-Station-Id providing MAC addresses, use of Acct-In/Output-Gigaword for accounting roll-over, Acct-Session-Id added to Access-Request,  and support for Session-Timeout.

<strong>Added WISPr XML</strong> support to assist devices and smart-clients in seamless authentication. The embedded XML provides instructions on how to login to non-browser based applications running on the client device. Usernames presented to WiFiDog will be parsed for a realm - which is then used by WiFiDog as the network name. So, for allowing a realm to roam, a "network" can be created with a RADIUS authenticator, for example.

<strong>MAC Authentication</strong> is being done using the pcap library (for now) and watching for DHCP replies. It is activated by specifying the MacAuthRealm configuration option in the wifidog.conf specifying the WiFiDog "network" to use for authentication and (currently) requires that the network is configured for RADIUS authentication in WiFiDog.

The changes are provided to (hopefully) raise the standards of WiFiDog with respect to RADIUS and WISPr generally, but are also required for <a href="/CoovaAAA/WiFiDog">use with CoovaAAA</a> - requiring more standardized RADIUS and access controller feature set. Of course, the patches are provided under the Gnu Public License and your <em>testing</em> and use is encouraged! Bring your questions and comments <a href="/Community">to the community</a>. Enjoy!
