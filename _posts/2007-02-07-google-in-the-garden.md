---
status: old
layout: post
title: Google in the garden
created: 1170876960
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
Google has a lot to offer when it comes to location specific and community information. With the latest release of CoovaAP firmware, some of these features are made easily available to assist in the configuring the latitude and longitude of your hotspot using <a href="http://maps.google.com/">Google Maps</a>, showing <a href="http://local.google.com/">local area Google Maps</a> in the embedded captive portal, and promoting of your hotspot in <a href="http://base.google.com/">Google Base</a>.

[img_assist|nid=349|title=|desc=|link=none|align=center|width=400|height=212]

As shown above, within the web configuration console you can configure your hotspot's exact latitude and longitude with the help of a map and movable marker showing the coordinates. This information can then be used by the local area map in the embedded captive portal to show visitors general area information, shown below.

[img_assist|nid=351|title=|desc=|link=none|align=center|width=350|height=336]

Visitors may find this useful. Of course, when they click for more information, they still need to login. But, how did they find your hotspot in the first place?

While the feature is still experimental, shown below in the web console of the firmware, you are able to configure a <a href="http://www.google.com/accounts/">Google Accounts</a> user's authentication token to list the hotspot (with geo-coordinates) in Google Base, demonstrated here in <a href="http://base.google.com/base/a/1498299/D13787293875126773478">this example</a>.

[img_assist|nid=353|title=|desc=|link=none|align=center|width=400|height=66]

While Google is in the walled garden, you can also show your own calendar of events from within the captive portal. First, get the Calendar HTML code you need; <a href="http://www.liewcf.com/blog/archives/2006/06/add-google-calendar-on-website/">explained here</a>. Next, pick the embedded portal page to insert the calendar into. Below, we place the HTML into the Login Page template.

[img_assist|nid=355|title=|desc=|link=none|align=center|width=400|height=246]

The calendar now appears on the login page. The events of our specific calendar are displayed and linked to more information.

[img_assist|nid=357|title=|desc=|link=none|align=center|width=400|height=341]

<p align="left">Sure, pretty much all of Google is in the walled garden. But, Google largely does not provide content - only links to other sites and services on the Internet. Is it worth it for you?</p>
<p align="left">What about ads? Check your terms of service before putting AdSense in the captive portal or frame - unless you are able to put all the advertisers in the walled garden.</p>
