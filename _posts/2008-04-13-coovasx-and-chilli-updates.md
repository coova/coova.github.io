---
status: old
layout: post
title: CoovaSX & Chilli updates
created: 1208153315
categories: []
---
<strong>Introducing CoovaSX</strong>

[img_assist|nid=201|title=|desc=|link=none|align=right|width=125|height=223]I recently acquired a <a href="http://europe.nokia.com/A4494164">Nokia N95 8GB</a> smartphone and started using the WiFi features before making my first voice call. I immediately was annoyed with my own captive portal and having to key in my username and password each time I wanted online - not to mention having to navigate a webpage not made for small displays. The picture on the right shows the embedded browser on my Facebook landing page.

The embedded browser would remember my username (until the cache gets cleared), but never my password. There is now an easier way to login your Java-capable smartphone to your captive portal hotspot - using <a href="http://www.coova.org/CoovaSX">CoovaSX 1.0</a>! Similar to the firefox extension <a href="http://www.coova.org/CoovaFX">CoovaFX</a>, but for your phone, <a href="http://www.coova.org/CoovaSX">CoovaSX</a> will log you into your hotspot without going through the captive portal. Configure your username and password once, then use <a href="http://www.coova.org/CoovaSX">CoovaSX</a> to login before using the Internet - all without using your browser.

[img_assist|nid=202|title=|desc=|link=none|align=center|width=439|height=210]

To use the application, your phone must support <a href="http://en.wikipedia.org/wiki/MIDlet">Java MIDlets</a> (MIDP-2.0). <a href="http://www.coova.org/CoovaSX">CoovaSX</a> works at hotspots with  a captive portal supporting the <a href="http://en.wikipedia.org/wiki/WISPr">WISPr</a> XML method of authentication. Visit us in <a href="http://www.coova.org/forum/">the forum</a> with your comments, questions, or suggestions.

<strong>CoovaChilli Update</strong>

Now in <a href="http://www.coova.org/CoovaChilli/SVN">subversion</a> are some updates to <a href="http://www.coova.org/CoovaChilli">CoovaChilli</a> - which include:
<ul>
	<li>New options <em>dhcpgateway</em> and <em>dhcpgatewayport</em> to specify a DHCP gateway (relay) host IP address and port,</li>
	<li>New option <em>dhcpradius</em> for mapping some DHCP options into RADIUS attributes and visa versa during MAC authentication, as <a href="http://www.coova.org/node/118">described here</a>,</li>
	<li>New internal state called <em>splash</em> in which clients are given Internet access, but enforcing the port 80 http redirect,</li>
	<li>New option <em>macauthdeny</em> which will result in the black-listing of devices given an Access-Reject during MAC address authentication, and</li>
	<li>Code cleanups, reorganization, and bug fixes.</li>
</ul>
Binaries will become available through <a href="http://www.coova.org/forum/">the forum</a>, where you can also report problems or offer suggestions. For more information on changes in Chilli, see the <a href="http://www.coova.org/CoovaChilli/ChangeLog">ChangeLog</a>.

<strong>Funding</strong>

Just like FON, with their <a href="http://blog.fon.com/en/archive/business/fon-raises-95-million.html">recent $9.5 million round of funding</a> (<a href="http://blog.marcelotoledo.org/2008/04/12/fon-raises-95-million-to-buy-their-grave/">commentary here</a>), Coova too needed to raise some money. Though, not on such a scale. We had to plop down an extra $550 for a 2 year code signing certificate from <a href="http://www.thawte.com/">Thawte</a> :) ...
