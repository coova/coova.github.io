---
status: old
layout: post
title: Pocket Hotspot
created: 1238217813
categories:
- !binary |-
  cmVsZWFzZXM=
- !binary |-
  YXBwbGljYXRpb25z
---

![Openmoko](/img/2009-03-27-pocket-hotspot/openmoko.png)
The  <a href="http://www.openmoko.com/product.html">Neo Freerunner</a> from <a href="http://www.openmoko.com/">Openmoko</a> is addictive. I would call it a "phone," but I haven't really used that feature much yet. It's simply a nice, very nice, pocket sized Linux system with touch-screen, <a href="http://en.wikipedia.org/wiki/General_Packet_Radio_Service">GPRS</a>, <a href="http://en.wikipedia.org/wiki/Global_Positioning_System">GPS</a>, and, of course, <a href="http://en.wikipedia.org/wiki/Wi-Fi">Wi-Fi</a>. My Freerunner came with <a href="http://www.android.com/">Google Android</a> on it, but I wanted to start out with <a href="http://wiki.openmoko.org/wiki/Om_2008.12_Update">Openmoko's own firmware</a>. With the latest version of their software, I found most  features of the phone operational, complete with a nice soft keyboard. It is also very easy to build applications for the phone, using standard GNU tools and GUI building in X/<a href="http://www.gtk.org/">GTK</a>.  There is even the <a href="http://www.pygtk.org/">Python GTK extensions</a> available for quick and easy GUI development - that can be reused in other distributions (Ubuntu, etc) too. All things considered, Openmoko has made an excellent open device and platform.

CoovaChilli Hotspot on the Freerunner
-------------------------------------

Building <a href="/CoovaChilli">CoovaChilli</a> for the Openmoko firmware was a simple matter of cross-compiling with the <a href="http://wiki.openmoko.org/wiki/Toolchain">Openmoko Toolchain</a>. Combined with a basic Python/GTK GUI to start, stop, and configure CoovaChilli, the <a href="http://www.opkg.org/package_176.html">CoovaChilli application</a>, now available at <a href="http://www.opkg.org/">opkg.org</a>, is all you need to run a Hotspot from your phone!

<strong>Start</strong> and <strong>Stop</strong> the WiFi Ad-Hoc Hotspot using one of several configurations.

![Image](/img/2009-03-27-pocket-hotspot/coova-status.png)

See <strong>Sessions</strong> and devices connected to your Ad-Hoc WiFi network. From here, you can see statistics, login state, and do various things like <strong>Auth</strong>orize, <strong>Release</strong>, or <strong>Block</strong> the session. Authorize means the visitor gets on-line (no captive portal), Release will forget the DHCP lease (and logout), and Block will drop all packets from the device.

![Image](/img/2009-03-27-pocket-hotspot/coova-sessions.png)

Maintain several CoovaChilli configurations that you can switch between. Perfect for testing or demonstrations - taking your Hotspot (and GPRS Internet) with you on the road, to school, work, and meetings. Also nice if you just want to selectively share your GPRS Internet.

![Image](/img/2009-03-27-pocket-hotspot/coova-config.png)

Edit the default configuration or create a new configuration profile. Start by using the <strong>Clone</strong> button (not shown, scroll down to see it), then change the setting to match your Hotspot network configuration.

![Image](/img/2009-03-27-pocket-hotspot/coova-config-edit.png)

To use with our free CoovaAAA service, change the RADIUS <strong>Shared Secret</strong> to match the one assigned to you by CoovaAAA, then login at least once into the captive portal using your CoovaAAA account from a computer connected to your Hotspot network. For other back-end providers, use the settings for CoovaChilli provided by them.

Enjoy!
