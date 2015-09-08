---
status: old
layout: post
title: New Coova Chilli Release
created: 1164313763
categories:
- !binary |-
  cmVsZWFzZXM=
---
New Coova ChilliSpot version 1.0-coova.3!
<ul>
	<li><a href="/CoovaChilli">Project Page</a></li>
	<li><a href="/Download">Download</a></li>
</ul>
Highlights in this release:
<ul>
	<li>Additional RADIUS support and features</li>
	<li>A "WPA Guest" feature for 802.1x captive portal</li>
	<li>A local users file for simple non-RADIUS authentication</li>
	<li>Restricting the walled garden to ports, not just hosts</li>
	<li>Support for post authentication HTTP proxy</li>
	<li>An external "chilli_response" utility</li>
</ul>
Thus far, I have been calling this a patch for <a href="http://chillispot.org/">ChilliSpot</a> 1.0, but it may be time to consider it a project  in its own right. Coova's chillispot is largely backward compatible with ChilliSpot 1.0, but less so with 1.1 only because of implementation differences with centralized RADIUS configurations. But, the <a href="/CoovaChilli/ChangeLog">list of features and fixes</a> that Coova Chilli adds is getting larger and hardly a "patch" any longer. It is still our goal to integrate as much as possible with ChilliSpot, but this is not always possible. We will see how it goes. If you have any questions, be sure to check out the <a href="/forum/">forum</a>.
