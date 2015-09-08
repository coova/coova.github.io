---
status: old
layout: post
title: Hardware, software, standards
created: 1208508216
categories: []
---
The idea behind Coova is simple: to provide you with the open (and free) tools and services you need to manage and access your WiFi network, just the way <em>you</em> want to. Our philosophy is that you shouldn't be required to use any specific hardware (like <a href="http://www.fon.com/en/">FON</a> or <a href="http://meraki.com/">Meraki</a>) or software (like <a href="http://www.whisher.com/">Whisher</a>). From the ground up, Coova is about being open and standards based - compatible with the widest possible range of hardware, protocols, and services. It's about bringing <a href="http://meraki.com/blog/2008/04/17/new-carrier-services/">"Carrier" grade</a> features and services to the open-source/services world. It's also about making dumb routers a bit smarter - recycling is good, right?

With Coova, you can pick and choose the software and services you need - depending on the kind of network you are building and how you want to access it. Here are some typical uses of Coova technologies:
<ul>
	<li>Use <a href="/CoovaAP">CoovaAP</a> for easy configuration of <a href="/CoovaChilli">CoovaChilli</a> (or <a href="http://dev.wifidog.org/">WiFiDog</a>):
<ul>
	<li>with or without using CoovaAAA services,</li>
	<li>using RADIUS or locally defined users,</li>
	<li>using the customizable "Internal" captive portal, or</li>
	<li>configured to use your own portal or RADIUS service.</li>
</ul>
</li>
	<li>Use <a href="/CoovaChilli">CoovaChilli</a> either in <a href="/CoovaAP">CoovaAP</a> or in your own firmware or server to:
<ul>
	<li>enforce a captive portal and authentication using CoovaAAA or any other portal/RADIUS service,</li>
	<li>works with a variety of commercial services (ask your provider),</li>
	<li>integrate with 802.1X authentication to provide accounting and access limitations.</li>
</ul>
</li>
	<li>Use <a href="/CoovaAAA">CoovaAAA</a> to manage the access to your network:
<ul>
	<li>with a <a href="/wiki/CoovaAAA_WithCoovaChilli">CoovaChilli/AP captive portal</a>,</li>
	<li>using a <a href="/wiki/CoovaAAA_WithWiFiDog">patched WiFiDog</a> captive portal,</li>
	<li>using <a href="/node/80">your own captive portal</a> (no advanced programming needed),</li>
	<li>using our <a href="/wiki/CoovaAAA_WithFacebook">Facebook</a> or <a href="/wiki/CoovaAAA_CaptivePortals">standard captive portal applications</a>,</li>
	<li>using a commercial access controller (like <a href="/wiki/CoovaAAA_WithColubris">Colubris</a>), or</li>
	<li>using any router supporting WPA Enterprise/802.1X (like the <a href="/wiki/CoovaAAA_WithAirPortExtremeBaseStation">AirPort Extreme</a>).</li>
</ul>
</li>
	<li>Use and share your <a href="/CoovaAAA">CoovaAAA</a> controlled network:
<ul>
	<li>using one account to login to both your captive portal and your secure WPA Enterprise networks (using any device supporting 802.1X, like <a href="/wiki/CoovaAAA_WithMacosx">your laptop</a> or <a href="http://coova.org/wiki/index.php/CoovaAAA/WPANokia">Nokia phone</a>),</li>
	<li>using your account at any <a href="/CoovaAAA">CoovaAAA</a> location that is being shared with you,</li>
	<li>selectively share your network with only those you choose - individuals or entire realms, or</li>
	<li>share your network based on <a href="/node/71">OpenID</a> logins or Facebook fans/friends.</li>
</ul>
</li>
	<li>Use <a href="/CoovaFX">CoovaFX</a> and <a href="/CoovaSX">CoovaSX</a> in Firefox or your phone, respectively, to login past a captive portal using the WISPr standard and a pre-configured account - WISPr is supported by CoovaAAA and most commercial access controllers and service providers.</li>
</ul>
<ul>
	<li>Use <a href="/JRadius">JRadius</a> to program your own RADIUS provisioning logic for your network.</li>
</ul>
If you are building a WiFi network and haven't found anything on this site that can help you, you probably haven't looked hard enough. Though, it has been said, and we do acknowledge, that more documentation is needed. For this, we call out to the development and user community to help out in <a href="/wiki/Main_Page">the Wiki</a> , <a href="/forum/">forums</a>, and <a href="/wiki/MailingLists">mailing lists</a>. Note: In the Wiki, we do lock pages to prevent SPAM - either create a new page or ask for more permissions on one of the mailing lists.

We are also hoping to hear more about how and where you are using Coova! In fact, a friend of mine was recently vacationing in the Dominican Republic and was pleasantly surprised to find a Coova signal at the Hotel. They were using CoovaAP for their WiFi. Stories like this are terrific -- lets get them in the forum!
