---
layout: post
title: New Chilli & Firmware
created: 1170874005
categories:
- !binary |-
  cmVsZWFzZXM=
---
New <strong>CoovaAP Firmware</strong> version 1.0-beta.4!
<ul>
	<li><a href="/CoovaAP">Project Page</a></li>
	<li><a href="/Download">Download</a></li>
</ul>
Highlights in this release:
<ul>
	<li>Updated <a href="http://openwrt.org/">OpenWrt</a> (WhiteRussian 0.9)</li>
	<li>ChilliSpot version 1.0-coova.4 (see below)</li>
	<li>Updated web console and embedded captive portal</li>
</ul>
New <strong>Coova ChilliSpot</strong> version 1.0-coova.4!
<ul>
	<li><a href="/CoovaChilli">Project Page</a></li>
	<li><a href="/Download">Download</a></li>
</ul>
Highlights in this release:
<ul>
	<li>Merged the so-called "Any IP" patch</li>
	<li>Several bug fixes as discussed in the <a href="/CoovaChilli/ChangeLog">ChangeLog</a></li>
</ul>
We are pleased to release both a new CoovaAP Firmware and Coova-Chilli.  Along with several bug fixes and improvements, Coova-Chilli now supports the "Any IP" feature whereby client devices can be configured with any static IP address. It goes without saying that this feature is now also in the firmware - now based on the officially released OpenWrt WhiteRussian 0.9.

<strong>Careful! </strong>when upgrade from a previous Coova firmware if you have any local users configured. Most router configurations are not stored in the file system and will remain intack. However, local users and other configuration like the embedded portal templates need to be backed up. So, be sure to <strong>save your current configuration</strong> from within the web admin console. Once you upgrade, go through the configuration pages to ensure all required packages are (re-)installed and everything looks ok.

As always, thanks to members of the <a href="/forum/">forum</a> for reporting bugs and making feature suggestions.
