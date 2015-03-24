---
layout: post
title: MAC Authentication
created: 1186394436
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
There is a new version of the free CoovaAAA service now running. You are now able to selectively configure your account in general, and then specific devices, for MAC Address Authentication! Of course, this only works with supported access controllers and configurations - so, for only <a href="/CoovaChilli">CoovaChilli</a> (or ChilliSpot) and <a href="/CoovaAAA/WiFiDog">WiFiDog</a> captive portals solutions - possibly others.  This feature does not work for WPA Enterprise, and not needed as most clients will likely auto-connect with your configured account information.

<strong>How to configure for MAC Authentication</strong>

When logged into <a href="https://coova.org/">https://coova.org/</a>, edit your Security Preferences to include <em>Allow MAC Authentication</em>, as shown below:

[img_assist|nid=335|title=|desc=|link=none|align=center|width=516|height=169]

Only if this user-level option is set will any device owned by the you be allowed to authenticate automatically.

<strong>Configuring your device</strong>

You may already have some devices associated with your account. Find your device which you added by logging in, using WPA or embedded captive portal configured for coova.org AAA, at least once before.

[img_assist|nid=337|title=|desc=|link=none|align=center|width=466|height=251]

Click on <em>edit</em> and then select the <em>Allow MAC Authentication</em> option. Setting this option means that your device will auto-authenticate using RADIUS at hotspots configured to perform MAC authentication with CoovaAAA services.

[img_assist|nid=339|title=|desc=|link=none|align=center|width=366|height=132]

You can't currently add client devices manually. That is a big limitation, I know, but some thought is required to prevent abuse. True, you can spoof RADIUS, but don't want to make it easy to harvest arbitrary MAC addresses. It requires some thought and anti-abuse measures. Suggestions, comments, and help requests <a href="/forum/">are welcomed</a>.

Note: Using this feature, of course, does not improve your account security! But, for many, a risk they are willing to take for the convenience.
