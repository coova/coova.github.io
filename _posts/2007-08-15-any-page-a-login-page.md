---
status: old
layout: post
title: Any page a login page
created: 1187185070
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
There is a new version of <a href="/CoovaChilli">CoovaChilli</a> in <a href="/wiki/BuildingCoovaChilli">SVN</a> that is getting close to being released as version 1.0.7. There are several fixes and new features, see the <a href="/CoovaChilli/ChangeLog">ChangeLog</a> for details. One cool feature added is the <a href="/CoovaChilli/JSON">JSON interface</a> which allows for easy communication for browser based captive portal applications. Meaning, using JavaScript it is possible to use any HTML page as your captive portal landing page just by adding one line of HTML code:
<pre>&lt;script&nbsp;id='chillijs'&nbsp;src='http://ap.coova.org/js/chilli.js'&gt;&lt;/script&gt;</pre>
When the page is used as the chilli login page, the script above attempts to load the <a href="http://dev.coova.org/svn/coova-chilli/www/ChilliLibrary.js">ChilliController</a>, javascript contributed by Yannick Deltroo (thanks!), and the default login form template. The ChilliController code and <a href="http://dev.coova.org/svn/coova-chilli/www/json_html.tmpl">default HTML template</a> are hosted by the chilli daemon directly - customizable on a per location basis. For instance, this <a href="http://ap.coova.org/uam/">simlpe captive portal page</a> (picture below) uses CSS to customize the user interface, as does this simple example:
<pre>&lt;style&gt;
&lt;!--
#chilliPage&nbsp;{
&nbsp;&nbsp;border:&nbsp;1px&nbsp;solid&nbsp;orange;
&nbsp;&nbsp;padding:&nbsp;20px;
&nbsp;&nbsp;margin-top:&nbsp;20px;
}
#signUpRow&nbsp;{
&nbsp;&nbsp;display:&nbsp;none;
}
--&gt;
&lt;/style&gt;
...
&lt;script&nbsp;id='chillijs'&nbsp;src='http://ap.coova.org/js/chilli.js'&gt;&lt;/script&gt;</pre>
All the elements of the form can be styled individually, or completely turned off like the sign-up link (element 'signUpRow') in the above example. The coova default landing page uses <a href="view-source:http://ap.coova.org/uam/">some simple CSS</a> to produce:

[img_assist|nid=331|title=|desc=|link=none|align=center|width=466|height=303]

A simple and interactive captive portal page. The ChilliController loads location information (like the location name, "My HotSpot" above), takes care of logging in (using CHAP challenge/response) and periodically checks for login status and session stats, producing:

[img_assist|nid=333|title=|desc=|link=none|align=center|width=466|height=305]

A captive portal login/status box like this can be easily embedded into any web page! I'm using my .Mac home page :) ... you get the point.

But, this version of chilli still needs some testing... and to be released soon. If you have a computer running Linux with two network interfaces (doesn't have to be WiFi, you know), <a href="/wiki/BuildingCoovaChilli">give it a try</a>! Bring your feedback to the <a href="/forum/">forum</a>.
