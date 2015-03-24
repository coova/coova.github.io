---
layout: post
title: Facebook; Social WiFi Utility
created: 1193726409
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
My <a href="/node/92">last post</a> was geared toward attracting the network administrators of communities, schools, or companies to come and roam with <a href="/CoovaAAA">CoovaAAA</a>. It would be awesome, for instance, if CoovaAAA users could selectively share their networks with the <a href="http://www.fon.com/en/">FON</a> community, their classmates at school, or colleagues at work. However, not all of these organizations use RADIUS and those who do are often unwilling to change their setup without strong financial incentives or demands from their users. Which got me thinking, many people these days are creating and linking their communities, colleagues, and friends using on-line "Social Utilities" like <a href="http://www.facebook.com/">Facebook</a>. I have been looking into the <a href="http://developers.facebook.com/">Facebook platform</a> and started integrating it with CoovaAAA. The result is turning out better than initially expected!

<strong>The Social WiFi Utility</strong>

<a href="http://www.facebook.com/">Facebook</a> has an interesting platform. I now realize that it being called a "Social Utility" isn't just marketing hype. With their <a href="http://wiki.developers.facebook.com/index.php/API">API</a>, <a href="http://wiki.developers.facebook.com/index.php/FBML">FBML</a>, <a href="http://wiki.developers.facebook.com/index.php/FBJS">FBJS</a>, and <a href="http://wiki.developers.facebook.com/index.php/FQL">FQL</a> technologies combined with the overall friends and network architecture, it is relatively straight forward to create an entire "social networking" application around Facebook or integrate their platform with another. Since CoovaAAA is about managing your WiFi network and sharing it with others, it makes sense to leverage the social network building features of Facebook to create a Social <em>WiFi</em> Utility.

This is made possible with a captive portal application built for the Facebook platform combined with the CoovaAAA authentication services.

<strong>The Facebook Application</strong>

Facebook enforces that all visitors are members as they are redirected to the Facebook <a href="http://www.facebook.com/apps/application.php?id=7108185615">Coova HotSpot</a> captive portal application. Facebook is placed in the HotSpot's walled garden, so all visitors are able to login and see the owner's profile - leaving a message or giving a "poke".

[img_assist|nid=309|title=|desc=|link=none|align=center|width=516|height=338]

Above is what you see when logged into Facebook, but not a friend of the HotSpot owner. Of course, the owner is always logged in automatically, so are friends, as shown below.

[img_assist|nid=311|title=|desc=|link=none|align=center|width=516|height=377]

The access point owner must have a Coova account (linked to their Facebook profile). Visitors don't need a Coova account, but also benefit from having one.

[img_assist|nid=313|title=|desc=|link=none|align=center|width=516|height=382]

With your Coova account linked to your Facebook profile, you are able to see your usage and perhaps manage your own Coova HotSpot - all from the embedded application.

<strong>Getting Started</strong>

The latest release of <a href="/CoovaChilli">CoovaChilli</a> or <a href="/CoovaAP">CoovaAP</a> is what is needed running on your router - be it Linux or Linksys (and some others).Â  You will find the <a href="/CoovaAAA/Facebook">documentation in the wiki</a> and you are able to get help in <a href="/forum/">the forum</a> or IRC (#coova at freenode.net).

(updated November 5)
