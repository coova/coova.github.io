---
layout: post
title: Access policies, codes, more
created: 1198060074
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
There is a new version of <a href="/CoovaAAA">CoovaAAA</a> deployed! The highlights:
<ul>
	<li>Ability to create access policies defining time and data limits</li>
	<li>Share with users or entire realms based on a policy</li>
	<li>Generate a limited number of access codes based on a policy</li>
	<li>Support for <a href="/CoovaChilli">CoovaChilli</a>/Chillispot data limits based on a policy</li>
	<li>Stopping stale sessions when the NAC reboots</li>
	<li>Updated Facebook and new general use captive portal</li>
	<li>Bug fix concerning WPA-only option</li>
</ul>
<strong>Access Policies</strong>

Access policies define how access is to be provisioned. With this release, you can set the amount of access time and/or the data limits granted in a certain time frame. For instance, a policy might be for 2 hours of access, with a data cap of 10G, to be used within 24 hours. Additionally, the policy can be configured as <em>recurring</em>; for instance, a policy for 2 hours per <em>any</em> 24 hour period. Use policies to limit the access of individual users or entire realms you are sharing with. This includes Facebook users when using the Facebook captive portal.

[img_assist|nid=299|title=|desc=|link=none|align=center|width=516|height=386]

This screenshot shows the look-and-feel of the Facebook embedded version and how users can individually be configured with an access policy. Similarly, in the next tab, <em>Share with realms</em>, you can configure entire realms with an access policy, specifying whether or not the limitation is for the entire realm (as in everybody has to share the same 2 hours) or if it should be <em>per user</em> (where a new <em>Allowed User</em> is added with the access policy).

<strong>Access Codes</strong>

In this release, you are able to create 10 access codes based on a access policy of your own. The limit is there while the feature is in <em>beta</em>.  When you create an access code, you are basically creating your own usernames and passwords linked to your access policy and network (your own access points). Below, showing the standard look-and-feel, you can see the new <em>Access</em> tab in the manager application and some sample access codes.

[img_assist|nid=301|title=|desc=|link=none|align=center|width=516|height=381]

Notice how access codes are considered under the realm "code" in the system. This is to not conflict with the default realm of users (i.e. the coova.org realm). Ultimately, when logging in to a network you need a username and password ("credentials"). For the access codes, this means the username, in theory, must be prefixed with this <tt>code</tt> realm according to <a href="/node/92">RADIUS specification</a>. That gets pretty technical. But, the new Facebook and general use captive portal in CoovaAAA makes it easy by providing a separate login dialog for both users and codes, as shown below. When logging in with an access code, the appropriate realm is automatically prepended.

<strong>Captive Portals</strong>

The Facebook captive portal was updated. Some adjustments were required as Facebook no longer enforces a login before viewing an application.

[img_assist|nid=303|title=|desc=|link=none|align=center|width=466|height=264]

Which is nice - since now it is easier to put a login box for Coova-enabled user and access code logins for when the visitor is not a Facebook member.

[img_assist|nid=305|title=|desc=|link=none|align=center|width=466|height=264]

With the same login box features of the Facebook application, there is now also a general use <a href="/CoovaChilli">CoovaChilli</a> captive portal login application. Similar to the embedded captive portal of CoovaChilli and <a href="/CoovaAP">CoovaAP</a>, but this hosted version will be expanded and updated more frequently. It can be used with your own RADIUS back-end or take advantage of the features offered through <a href="/CoovaAAA">CoovaAAA</a> - including <a href="/node/71">OpenID authentication</a> (enabled as an option).

[img_assist|nid=307|title=|desc=|link=none|align=center|width=416|height=174]

Learn <a href="/wiki/CoovaAAA_CaptivePortals">more about this</a> newest addition to the Coova <a href="/wiki/Hotspot_Development_Kit"><em>hotspot development kit</em></a>. I'm thinking of calling it this as everything Coova can not only be used as a whole, but also as bits and pieces. With more and more bits and pieces coming in the form of software, tools, resources, and services! If you find any problems or have suggestions, let us know in <a href="/forum/">the forum</a>.
