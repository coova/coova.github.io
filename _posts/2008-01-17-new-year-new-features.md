---
layout: post
title: New Year; New Features
created: 1200569308
categories:
- !binary |-
  cmVsZWFzZXM=
---
<strong>Happy new year!</strong>

To bring in the new year, there are new features already live in <a href="/CoovaAAA">CoovaAAA</a> and some interesting <a href="/CoovaChilli">CoovaChilli</a> development in progress.  As mentioned on the mailing list, CoovaAAA now has the following features:
<ul>
	<li>basic session history graphing</li>
	<li>basic access point bandwidth graphing</li>
	<li>downloading of session data</li>
	<li>access point monitoring notifications</li>
	<li>"open access" MAC address authentication</li>
	<li>updated <a href="/wiki/CoovaAAA_Desktop">CoovaAAA Desktop</a> application</li>
</ul>
The bandwidth graphing and monitoring notification features currently require CoovaChilli. The "open access" feature requires MAC address authentication and currently supports <a href="/CoovaChilli">CoovaChilli</a> and Colubris access controllers.

[img_assist|nid=289|title=|desc=|link=none|align=center|width=465|height=300]

Above, you can see the settings for an access point. If you are using a supported access controller, then the type and basic settings (like reversed accounting) have likely been auto-detected. Note that the bandwidth graph and monitoring alerts are only available currently for CoovaChilli.

<strong>Open Access, with Accounting</strong>

With open access enabled in CoovaAAA and MAC address authentication configured in the access controller, visitors to your HotSpot are automatically authenticated and given Internet access. Give access to anybody, anonymously, by adding the special <em>anonymous</em> realm to your <em>Allowed Realms</em>, as shown below.

[img_assist|nid=291|title=|desc=|link=none|align=center|width=465|height=300]

The user experience is no different from an open access point, but you benefit from session and usage accounting.

<strong>Graphing & Downloading Sessions</strong>

CoovaAAA now has graphs! For the simple session summary graph, <a href="http://www.jfree.org/jfreechart/">JFreeChart</a> is being used - an excellent and easy to use open-source charting library. The graph shows the number of sessions and minutes per day, based on the start time of the session.

[img_assist|nid=293|title=|desc=|link=none|align=center|width=466|height=291]

This is perhaps not always ideal since sessions can last longer than a day and you don't necessarily want to graph all that time in one day. Above is an example of the graph showing a mixture of access controller types. Of course, if the access controller doesn't support RADIUS accounting, like many commercial WPA Enterprise routers, you will not see any minutes for those sessions.

In the same window, you can now download the selected sessions in a comma separated value (CSV) data file. This data file contains Session ID, Username, Realm, Status, Start time, Stop time, Duration, Bytes down, Bytes up, Device, Location, and other attributes taken from RADIUS.

Want to see the overall usage in CoovaAAA so far this month?

[img_assist|nid=295|title=|desc=|link=none|align=center|width=416|height=242]

(Note: A time-zone conversion issue has been noted where the graph is showing, for example, some sessions on December 31, when the graph should start on January 1st. The system time-zone is US Pacific, my profile is set to Central European Time.)

<strong>Graphing Access Point Bandwidth</strong>

CoovaChilli can be configured to authenticate itself as an <em>Administrative-User</em> (indicated in the RADIUS <em>Service-Type</em> attribute). This provides a convenient way for chilli to retrieve configuration settings from the RADIUS back-end. Using this RADIUS session, chilli sends global accounting of all running sessions back to the RADIUS server. These accounting requests can be, as they are in CoovaAAA, used for monitoring purposes and/or bandwidth graphing.

[img_assist|nid=297|title=|desc=|link=none|align=center|width=466|height=339]

For the data collection and graphing, <a href="http://www.jrobin.org/index.php/Main_Page">JRobin</a> is being used - providing a pure Java RRD (round-robin database) similar to that <a href="http://oss.oetiker.ch/rrdtool/">RRDTool</a>.

<strong>CoovaChilli Development</strong>

Last year, I mentioned some interesting features for CoovaChilli which are now in development. To summarize, a number of people in the <a href="/forum/">forum</a> have asked about less restrictive "splash page only" features - where visitors have full Internet access, but with an initial splash page when visitors are web browsing. To provide this, chilli will have a new internal state (not surprisingly called <em>splash</em>)  whereby visitors who are otherwise authorized are redirected to a splash page - either the chilli <em>uamserver</em> setting or a session specific URL.

There will be two ways to put a session into this state: 1) with a RADIUS <em>ChilliSpot-Config=splash</em> attribute in the <em>Access-Accept</em> (during MAC authentication, for instance), and 2) using the <a href="/CoovaChilli/chilli_query"><em>chilli_query</em></a> command line utility. To ensure the visitor has been to the splash page, chilli will still require a (re-)authentication via RADIUS to resume full authorized access. To some, it may seem over-kill to require a RADIUS authentication for a splash page acknowledgment. However, doing it this way provides a bit of proof of the acknowledgment in the back-end while also giving the opportunity to reconfigure session provisioning parameters.

Per default, when you use MAC authentication with chilli, an <em>Access-Reject</em> means that the visitor failed to authenticate by MAC address, but still may proceed to the captive portal where they can login. There will be a new option, called <em>macauthdeny</em>, to have chilli ignore all traffic from visitors given an <em>Access-Reject</em> during MAC address authentication - thereby <a href="http://en.wikipedia.org/wiki/Blacklist">black-listing</a> the device.

<strong>Other Development</strong>

On a completely different topic, I have recently been working with <a href="http://www.faqs.org/rfcs/rfc3588.html">Diameter</a> and came across this <a href="http://i1.dk/JavaDiameter/">JavaDiameter</a> project. The library provides a very nice pure Java (except for the optional <a href="http://i1.dk/JavaSCTP/">JavaSCTP</a> layer which does use a JNI library) Diameter stack. The API is rather perfect for building a <a href="http://tools.ietf.org/html/rfc4005#section-9">RADIUS/Diameter gateway</a> using <a href="/JRadius">JRadius</a>!
