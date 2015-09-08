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
<!--break-->
[img_assist|nid=269|title=|desc=|link=none|align=right|width=250|height=141]
<p>The  <a href="http://www.openmoko.com/product.html">Neo Freerunner</a> from <a href="http://www.openmoko.com/">Openmoko</a> is addictive. I would call it a "phone," but I haven't really used that feature much yet. It's simply a nice, very nice, pocket sized Linux system with touch-screen, <a href="http://en.wikipedia.org/wiki/General_Packet_Radio_Service">GPRS</a>, <a href="http://en.wikipedia.org/wiki/Global_Positioning_System">GPS</a>, and, of course, <a href="http://en.wikipedia.org/wiki/Wi-Fi">Wi-Fi</a>. My Freerunner came with <a href="http://www.android.com/">Google Android</a> on it, but I wanted to start out with <a href="http://wiki.openmoko.org/wiki/Om_2008.12_Update">Openmoko's own firmware</a>. With the latest version of their software, I found most  features of the phone operational, complete with a nice soft keyboard. It is also very easy to build applications for the phone, using standard GNU tools and GUI building in X/<a href="http://www.gtk.org/">GTK</a>.  There is even the <a href="http://www.pygtk.org/">Python GTK extensions</a> available for quick and easy GUI development - that can be reused in other distributions (Ubuntu, etc) too. All things considered, Openmoko has made an excellent open device and platform.</p>
<p><strong>CoovaChilli Hotspot on the Freerunner</strong></p>
<p>Building <a href="/CoovaChilli">CoovaChilli</a> for the Openmoko firmware was a simple matter of cross-compiling with the <a href="http://wiki.openmoko.org/wiki/Toolchain">Openmoko Toolchain</a>. Combined with a basic Python/GTK GUI to start, stop, and configure CoovaChilli, the <a href="http://www.opkg.org/package_176.html">CoovaChilli application</a>, now available at <a href="http://www.opkg.org/">opkg.org</a>, is all you need to run a Hotspot from your phone!</p>
<table border="0" width="100%">
	<tr>
		<td valign="top"><strong>Start</strong> and <strong>Stop</strong> the WiFi Ad-Hoc Hotspot using one of several configurations.</td>
		<td align="right" valign="top">
[img_assist|nid=268|title=|desc=|link=none|align=left|width=320|height=240]</td>
	</tr>
	<tr>
		<td colspan="2"></td>
	</tr>
</table>
<table border="0" width="100%">
	<tr>
		<td valign="top">See <strong>Sessions</strong> and devices connected to your Ad-Hoc WiFi network. From here, you can see statistics, login state, and do various things like <strong>Auth</strong>orize, <strong>Release</strong>, or <strong>Block</strong> the session. Authorize means the visitor gets on-line (no captive portal), Release will forget the DHCP lease (and logout), and Block will drop all packets from the device.</td>
		<td valign="top">
[img_assist|nid=267|title=|desc=|link=none|align=left|width=320|height=240]</td>
	</tr>
	<tr>
		<td colspan="2"></td>
	</tr>
</table>
<table border="0" width="100%">
	<tr>
		<td valign="top">Maintain several CoovaChilli configurations that you can switch between. Perfect for testing or demonstrations - taking your Hotspot (and GPRS Internet) with you on the road, to school, work, and meetings. Also nice if you just want to selectively share your GPRS Internet.</td>
		<td valign="top">
[img_assist|nid=266|title=|desc=|link=none|align=left|width=320|height=240]</td>
	</tr>
	<tr>
		<td colspan="2"></td>
	</tr>
</table>
<table border="0" width="100%">
	<tr>
		<td valign="top">Edit the default configuration or create a new configuration profile. Start by using the <strong>Clone</strong> button (not shown, scroll down to see it), then change the setting to match your Hotspot network configuration.</td>
		<td valign="top">
[img_assist|nid=265|title=|desc=|link=none|align=left|width=320|height=240]</td>
	</tr>
	<tr>
		<td colspan="2"></td>
	</tr>
</table>
<p>To use with our free <a href="/CoovaAAA">CoovaAAA</a> service, change the RADIUS <strong>Shared Secret</strong> to match the one assigned to you by CoovaAAA, then login at least once into the captive portal using your CoovaAAA account from a computer connected to your Hotspot network. For other back-end providers, use the settings for CoovaChilli provided by them.</p>
<p>Enjoy!<br />
