---
layout: post
title: OpenID WiFi
created: 1181300046
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
With the newest release of <a href="/CoovaAP">CoovaAP</a>, some <a href="/CoovaChilli/ChangeLog">new features</a> in  <a href="/CoovaChilli">Chilli</a> are demonstrated in combination with <a href="/CoovaAAA">RADIUS</a> to allow <a href="http://openid.net/">OpenID</a> based authentication. If you are not yet familiar with OpenID, it is a distributed authentication protocol whereby you use a URL for your identity. This URL might be your <a href="http://www.livejournal.com/openid/about.bml">LiveJournal page</a>, from your <a href="https://www.myopenid.com/">MyOpenID account</a>, or <a href="http://simonwillison.net/2006/Dec/19/openid/">any page</a> you desire. Once logged in, your federated identity is valid across many websites. Now it can be used for WiFi access too.

[img_assist|nid=341|title=|desc=|link=none|align=center|width=516|height=404]

Above is the OpenID login form in CoovaAP's embedded captive portal. Instead of a traditional username and password, the user's OpenID URL is entered. When the form is submitted, the OpenID is sent to the RADIUS server (as a username). The RADIUS server, knowing that OpenID was turned on in access point (see below), will discover the OpenID authentication server for this URL and update the user's (session specific) walled garden before redirecting the user to their OpenID server to log in and grant permission (trust) to Coova.org.

To give an example, I signed up with LiveJournal and configured my personal home page with the following HTML:
<pre>&lt;html&gt;
&lt;head&gt;
&lt;link rel="openid.server"
&nbsp;&nbsp;href="http://www.livejournal.com/openid/server.bml"&gt;
&lt;link rel="openid.delegate"
&nbsp;&nbsp;href="http://wlanmac.livejournal.com/"&gt;
...</pre>
This will allow me to use my own URL while actually using my LiveJournal identity to log in everywhere. Now, when I log in to the captive portal with my homepage URL, I get authenticated at LiveJournal. Here's a sample of what their confirmation page looks like after logging in, if not already.

[img_assist|nid=343|title=|desc=|link=none|align=center|width=466|height=308]

Once permission is granted for this "calling" URL, in this case at coova.org, you are redirected back and logged in to the access point.

<strong>Using OpenID with Coova</strong>

[img_assist|nid=345|title=|desc=|link=none|align=right|width=346|height=430]CoovaAP version beta-1.5 or newer is required for this setup. The HotSpot RADIUS settings must also be configured (as per default) to coova.org. If you have a <a href="https://coova.org/">CoovaAAA account</a>, then use those RADIUS settings. Otherwise, the "coova-anonymous" shared secret <em>can</em> be used.

Using the web interface, configure the HotSpot RADIUS settings making sure <em>Allow OpenID Authentication</em> is <em>Enabled</em>, as shown here. On this same screen, you can now also configure the default session time and idle timeout - to be used when not otherwise set by RADIUS. Save and apply your changes.

With OpenID enabled and using the internal captive portal, a link to the OpenID login form is placed in the default login page. The templates for these pages can be customized in HotSpot / Portal of the web admin.

If you are using your CoovaAAA RADIUS settings, then you will see OpenID sessions, along with everything else.

[img_assist|nid=347|title=|desc=|link=none|align=center|width=616|height=378]

Well, that's it! Enjoy... and <a href="/forum/">let us know</a> how it goes.
