---
status: old
layout: post
title: Project news
created: 1206887007
categories:
- !binary |-
  dW5jYXRlZ29yaXplZA==
---
<strong>CoovaChilli & CoovaAP support</strong>

It is great to see <a href="/CoovaChilli">CoovaChilli</a> and <a href="/CoovaAP">CoovaAP</a> being used and supported by more companies and projects! <a href="http://www.fon.com/en/">FON</a> <a href="http://fonblog.wordpress.com/2007/08/27/la-fonera-hack-it-if-you-can/">has been using CoovaChilli</a>, <a href="http://www.open-mesh.com/roadmap.php">Open-Mesh.com plans to</a>, supported by <a href="http://worldspot.net/wk/en/Doc#Coova">Worldspot</a>, and Coova officially <a href="http://www.open.com.au/radiator/features.html">works with Radiator</a>. In fact, CoovaChilli will work with any RADIUS server and it is used by countless wireless ISPs, of all sizes, around the world. <a href="/CoovaAP">CoovaAP</a>, an <a href="http://openwrt.org/">OpenWrt</a>-based firmware for commodity WiFi routers, provides an easy to configure platform for CoovaChilli access controlled networks and <a href="http://www.nycwireless.net/supernode/">WiFiDog captive portal community networks</a> alike.

<a href="http://www.wifi-cpa.com/services.php">WiFi-CPA</a>, a commercial hotspot service company, also uses CoovaChilli and CoovaAP, though it might not be as obvious. They <a href="http://wifi-cpa.com/ScreenShots/accesspoint_admin_gui3.png">re-branded</a> and modified CoovaAP (which is not ideal, but ok when done right), <strike>took and doctored a diagram from this website</strike> (removed; thanks!), <strike>yet don't even mention or link to Coova.org</strike> (also remedied). They say imitation is a form of flattery; what about copyright infringement? There is also some confusion around the <a href="http://chillispot.info/">chillispot.info</a> website. As far as I can tell, this is a copy of the original ChilliSpot.org website (with commercial links added) and <em>is not</em> continuing with any development. It does, however, provide a <a href="http://www.chillispot.info/chilliforum/index.php">forum</a> for ChilliSpot die-hards, which is helpful for some.

Here at Coova, development is continuing toward a 2.0 release (for both CoovaChilli and CoovaAP), with the emphasis being on stability, performance, and remote manageability -- in addition to new features, including those described <a href="/node/118">here in the blog</a> and perhaps <a href="/forum/">here in the forum</a>; not to mention ideas for mesh integration. As with many open-source projects, community involvement, commercial support, and feature 'sponsorships' are important and welcomed. Thanks to all those who submitted bug reports, suggestions, or patches in the <a href="/forum/">forum</a>!

<strong>JRadius & FreeRADIUS user interface</strong>

I have been using <a href="http://www.freeradius.org/">FreeRADIUS</a> for some time - usually as the front-end to a <a href="/JRadius">JRadius</a> server. FreeRADIUS is both powerful and flexible, but I believe many would agree that what it needs most is a graphical user interface. It could also benefit from pre-cooked configurations for typical deployments. Indeed, the same could be said for JRadius and the configuring of it's handers. Perhaps CoovaEWT can be of assistance. <a href="/CoovaEWT">CoovaEWT</a> is a web-based user interface framework that is in development. The "compiled" Ajax (javascript/html) application is free to use and highly extensible using <a href="http://en.wikipedia.org/wiki/XML">XML</a> and <a href="http://en.wikipedia.org/wiki/XSL_Transformations">XSLT</a>. The user interface definition itself, the configuration it edits, and the scripts to generate the final application configuration files (e.g. radiusd.conf) are all customizable server-side files. Below are some screen-shots of what's in development in JRadius.

[img_assist|nid=279|title=|desc=|link=none|align=center|width=566|height=229]

Above is a typical screen from the FreeRADIUS administration interface - to configure the <em>interfaces</em>, in this case.

[img_assist|nid=281|title=|desc=|link=none|align=center|width=566|height=314]

In addition to configuring the FreeRADIUS server itself, the user interface is ideal to manage the database tables that come with the SQL module.

[img_assist|nid=283|title=|desc=|link=none|align=center|width=566|height=314]

Backed by the <a href="http://www.coova.org/JRadius/Dictionary">JRadius dictionary</a>, which is generated from FreeRADIUS dictionary files, the interface is able to help you complete attribute names, so you don't make any spelling mistakes. More news to come... stay tuned to the <a href="http://www.coova.org/JRadius">JRadius wiki</a>, <a href="http://www.coova.org/forum/">forum</a>, and <a href="http://www.coova.org/MailingLists">mailing list</a>.

<strong>CoovaFX on the road</strong>

For fun on a recent trip to London, I took a couple screen-shots of the WISPr-enabled networks <a href="http://www.coova.org/CoovaFX">CoovaFX</a> picked up in various places. I used CoovaFX to log into my hotel network with a voucher username and password I had to buy (boy, WiFi is expensive in London).

[img_assist|nid=285|title=|desc=|link=none|align=right|width=473|height=43]

[img_assist|nid=287|title=|desc=|link=none|align=right|width=436|height=43]

<p style="clear: both"></p>
