---
layout: post
title: Content-injection, Layer3
created: 1294411299
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
'''Content-injection''', as used in this article, means the inserting of HTML content into web pages going through a router. The idea is not new, and can be done in a variety of ways. Indeed, you might recall that years ago I did something similar using [http://transproxy.sourceforge.net/ transproxy] and [http://www.privoxy.org/ privoxy], which I called the [http://www.google.com/search?q=coova+captive+frame coova captive frame]. With developments in [[CoovaChilli]] and the interest in ad-paid WiFi, it's time to review the feature once again, this time natively in [[CoovaChilli]]. 

[[CoovaChilli]] introduced the concept of the external ''chilli_redir'' daemon in order to implement selective proxying of requests that match certain regular expressions against the request HTTP headers. This feature, for instance, can allow you do selectively add to your walled garden not just based on IP address and port, but also the URL path. Expanding on this proxy server feature, [[CoovaChilli]] now has the ability to '''inject content''' into HTTP requests that run through it's proxy. 

Keeping the injected HTML to a minimum, I decided to take advantage of the HTML script tag and to load a small [http://code.google.com/webtoolkit/ GWT] application into every ''text/html'' HTML content response. Going through [[CoovaChilli]]'s proxy server, our locally served (by chilli) application looks to be from the same server as that serving the HTML (therefore, avoiding any browser security issues). 

<code>
 
 <script src='/www/com.coova.Cd/com.coova.Cd.nocache.js'></script>
 
</code>

To illustrate with an real example, here is a [http://code.google.com/webtoolkit/ GWT] application that creates a dynamic top banner. 

[img_assist|nid=4650|title=|desc=|link=none|align=center|width=550|height=415]

In the banner, we just put our logo, but just about anything is possible. Tapping into the [[CoovaChilli JSON|JSON API]] already in [[CoovaChilli]], this application can be used to login. 

[img_assist|nid=4652|title=|desc=|link=none|align=center|width=550|height=415]

When logged in, it can show the session accounting information, also thanks to the JSON API. 

[img_assist|nid=4654|title=|desc=|link=none|align=center|width=550|height=415]

===Layer3 Only===

While discussing new features, one that is maturing nicely is Layer3 Only operation. Traditionally, [[CoovaChilli]] only operated at a Layer2 level - directly handling all ARP and DHCP. Internally, chilli maintains a one-to-one relationship between MAC address and IP address of subscribers. When you build with ''--enable-layer3'' (and run with run-time argument ''--layer3'') this all changes. [[CoovaChilli]] will no longer handle Layer2 and will only track subscriber sessions based on IP address. 

Looking for custom features, firmware, or back-end solutions? [mailto:support@coova.com contact coova for details...]
