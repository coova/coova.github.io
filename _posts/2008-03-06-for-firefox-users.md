---
status: old
layout: post
title: For Firefox Users
created: 1204815913
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
There is a standard known to some as <a href="http://blog.marcelotoledo.org/2007/12/27/wispr-spec-wireless-isp-roaming/">WISPr XML</a> - which provides a convenient way for non-browser based authentication on captive portal networks. The technique is used by a variety of smart-client and access controller vendors. <a href="/CoovaChilli">Chilli</a>, as an access controller, has long had support for WISPr; initially funded by <a href="http://www.weroam.com/">WeRoam</a> in the original ChilliSpot. Support for WISPr continues in <a href="/CoovaChilli">CoovaChilli</a>, and here is how to use it. To test and use this method of authentication to login, albeit, from the browser, install the new <strong><a href="/CoovaFX">Coova Firefox Extension</a></strong>. Tested against <a href="/CoovaAP">CoovaAP</a> and <a href="http://www.colubris.com/">Colubris</a>, it should work with any WISPr implementation.

[img_assist|nid=204|title=|desc=|link=none|align=right|width=166|height=203][img_assist|nid=203|title=|desc=|link=none|align=right|width=161|height=45]What does it do? First, the extension checks to see if you are online. It does this by trying to access a page on the Internet - a page not in the walled garden. At Hotspots supporting WISPr, the access controller sends back some XML along with the initial browser redirect to the captive portal. Smart-client applications use this information, which includes the hotspot location name,  to login to the network. This extension does the same thing, plus it:
<p style="clear: both"></p>

[img_assist|nid=198|title=|desc=|link=none|align=right|width=266|height=193][img_assist|nid=205|title=|desc=|link=none|align=right|width=126|height=41]
<div>
<ul>
	<li>shows the location name of the hotspot in the status bar,</li>
	<li>shows the duration of your session when logged in,</li>
	<li>will optionally remember your username and password,</li>
	<li>can automatically login to a hotspot on start-up,</li>
	<li>shows session status info if controller is chilli (using <a href="CoovaChilli/JSON">JSON</a>)</li>
	<li>helps test WISPr implementations.</li>
</ul>
</div>
<p style="clear: both"></p>
