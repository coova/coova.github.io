---
layout: post
title: New CoovaAP Firmware
created: 1164875594
categories:
- !binary |-
  cmVsZWFzZXM=
---
New CoovaAP firmware version 1.0-beta.3!
<ul>
	<li><a href="/CoovaAP">Project Page</a></li>
	<li><a href="/Download">Download</a></li>
</ul>
Highlights in this release:
<ul>
	<li>Updated <a href="http://openwrt.org/">OpenWrt</a> (WhiteRussian RC6)</li>
	<li>Updated web console and HotSpot configuration</li>
	<li>New Coova Chilli and other additional packages</li>
	<li>A completely <a href="/CoovaAP/EmbeddedCaptivePortal">embedded and customizable captive portal</a></li>
	<li>Option to use the "MAC Allowed" list without RADIUS authentication</li>
	<li>Web console and embedded captive portal using SSL</li>
	<li>Support for post authentication HTTP proxy</li>
</ul>
Yeah, that's right, a completely embedded simple captive portal using coova chilli that you can easily customize in the HotSpot web console! You can use it for simple Terms of Service acknowledgment, for allowing only your pre-configured users, or allow for self-registration. Just be sure to "backup" your router before reflashing it next time - otherwise you lose your user accounts!

Why release our own firmware instead of just packages for OpenWrt you ask? Well, the hope is that soon our packages will work on the standard OpenWrt image. I am working with our friends at <a href="http://openwrt.org">OpenWrt</a> and <a href="http://www.x-wrt.org/">X-Wrt</a> to better organize and integrate applications and packages like the Coova HotSpot with their projects. Ideally, applications from all sorts of independent projects (vendors, distributors, or company internal) can be add-ons to the standard web interface, providing the additional and tightly integrated configuration screens for the specific application.

Enjoy! and give us some <a href="/forum/">feedback</a>!
