---
layout: post
title: WiFi Roaming
created: 1193050377
categories: []
---
There are at least two meanings of <em>WiFi Roaming</em>. First, there is the physical hand-over of a client device from one access point to another - like perhaps in a mesh network. The other, and the one this article is about, refers to authentication, authorization, and accounting (AAA) roaming. Access controllers, like <a href="/CoovaChilli">CoovaChilli</a>, authenticate users and provide session usage accounting using <a href="http://en.wikipedia.org/wiki/RADIUS">RADIUS</a>. Through the RADIUS server, access is provisioned with or without session time or usage limitations and session statistics are collected.

[img_assist|nid=315|title=|desc=|link=none|align=center|width=539|height=234]

<em>RADIUS Roaming</em>, or <em>Realm-based Roaming</em>, is a feature of the RADIUS protocol whereby messages are forwarded by proxy to a remote 3rd party for processing based on a <em>Realm</em>. A realm in RADIUS is like the domain name in an e-mail address. It specifies the <em>Home Provider</em> of a user identified by a username and is usually formatted in one of two ways: as a prefix realm (e.g. <tt>realm/username</tt>), or like an e-mail address with a suffix  realm (e.g. <tt>username@realm</tt>).

<strong>RADIUS Roaming</strong>

In <a href="/CoovaAAA">CoovaAAA</a>, when you allow the realm coova.org access (on the <em>Sharing</em> page of the web interface), you are allowing other Coova users to get access using your network. It is also possible to grant login permission to other realms using remote RADIUS servers. If you have a user community (with a RADIUS server) and want to enable roaming with coova.org, <a href="mailto:support@coova.org">contact us</a>! It's a great - and free - way to share with the community you already know; you're own.

[img_assist|nid=317|title=|desc=|link=none|align=center|width=563|height=234]

If your RADIUS server does not support EAP protocols, or they are just too cumbersome to setup, CoovaAAA can help by terminating the EAP-TTLS tunnel and doing proxy for the "inner" tunneled authentication. This way, you can still get the benefits of WPA Enterprise / 802.1X without having to upgrade or reconfigure your current RADIUS installation.

[img_assist|nid=319|title=|desc=|link=none|align=center|width=539|height=223]

When using EAP-TTLS based protocols, you essentially establish a SSL connection (over UDP) directly to the RADIUS server. Over this tunnel, "inner" authentication can be performed using the user's true username and password. The "Supplicant," or client software (the internal Macos X Internet Connect or <a href="http://www.securew2.com/">SecureW2</a> for windows, for instance) establishes this connection and verifies the certificate of the RADIUS server it is talking to. If trusted, then authentication is performed.

<strong>RADIUS Accounting</strong>

RADIUS provides a means of accounting for the time and data consumed by users. It does this following various RFCs in order to be compatible with other vendors of similar products. Unfortunately, the meaning of what a client has sent versus what they received (in the form of <em>Input</em> or <em>Output</em> RADIUS attributes), can be reversed <a href="/wiki/CoovaChilli_RADIUS">depending on vendor and configuration</a>.

[img_assist|nid=321|title=|desc=|link=none|align=center|width=626|height=165]

To maintain consistency, <a href="/CoovaAAA">CoovaAAA</a> now allows the option <em>Reverse Accounting</em> when editing an Access Point - which defaults to <em>enabled</em> for compatibility. When proxying, <a href="/CoovaAAA">CoovaAAA</a> will send the correct values (reversing them if required) per RFC 2866. For more information, see the <a href="/CoovaAAA_RADIUSRequirements">CoovaAAA RADIUS requirements</a>.

<strong>CoovaChilli Accounting</strong>

Yes, the default accounting in <a href="/CoovaChilli">CoovaChilli</a> is reversed from ChilliSpot and now less-than RFC compliant. This was done, believe it or not, for <a href="/wiki/CoovaChilli_RADIUS">compatibility reasons</a>. However, since the first "coova" version, accounting is reversible back with the <em>swapoctets</em> option. If you use the <em>swapoctets</em> option with CoovaAAA, be sure to un-check the <em>Reversed Accounting</em> option for the Access Point.
