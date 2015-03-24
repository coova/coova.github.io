---
layout: post
title: Mesh, GUI, Chilli, AP
created: 1218200974
categories:
- !binary |-
  dW5jYXRlZ29yaXplZA==
---
<a href="/CoovaChilli">CoovaChilli</a>, the open-source access controller, is getting better all the time. Thanks go out to the growing <a href="/forum/">forum</a>, <a href="/MailingLists">mailing list</a>, and <a href="/wiki/IRC">IRC</a> communities for valuable patches and ideas! There is no wonder, then, why CoovaChilli continues to be used in more networks; municipal, mesh, and individual. I hear that <a target="_blank" href="http://www.moovera.com/">Moovera</a> is using it, and I have been helping out <a target="_blank" href="http://open-mesh.com/">Open-mesh.com</a> in integrating it. If you have more success stories, please do share. We like hearing about that sort of stuff.

<strong>Open-mesh.com</strong>

With Open-mesh, you are able to select one of several pre-defined service providers using the dashboard. They will also follow up with a more generalized configuration option for using your own RADIUS and captive portal settings. You can now select CoovaAAA, our free hotspot AAA service, to manage your open-mesh hotspots <a href="/CoovaAAA/OpenMesh">by following these instructions</a>. This will use Coova's basic login form captive portal. Once the more generic configuration option is available, then you will be able to utilize any Portal / RADIUS combination - including <a href="/node/135">Drupal</a> and Facebook.

[img_assist|nid=180|title=|desc=|link=none|align=center|width=500|height=219]

For assistance, feel free to join the <a href="/forum/">forum</a> or a <a href="/MailingLists">mailing list</a>, after <a href="/CoovaAAA/OpenMesh">rereading the directions</a>.

<span style="font-weight: bold">CoovaEWT</span>

<a href="http://www.coova.com/CoovaEWT">CoovaEWT</a> is our web-based configuration system. It comprises of two main pieces: the web application and the web services that drive it. The web application itself is pure static HTML and Javascript - able to run in any web container (browser, <a target="_blank" href="http://www.adobe.com/products/air/">Adobe AIR</a>, <a target="_blank" href="http://webkit.org/">WebKit</a>, <a target="_blank" href="http://developer.mozilla.org/en/docs/XULRunner">XULRunner</a>, <a target="_blank" href="http://developer.mozilla.org/en/docs/Building_an_Extension">Firefox add-on</a>, etc).

The web application uses Ajax calls against the EWT web services to build the user interface screens, get and save configurations, and can do wizard like interactive dialogs. A wide range of user interfaces are able to be defined in XML and shell scripts that reside on each device - accessible by  a single web application.

[img_assist|nid=179|title=|desc=|link=none|align=right|width=200|height=130]<span style="font-weight: bold">CoovaFX w/ EWT</span>

A recent snapshot of the CoovaEWT web application is includes in the just released <a href="/wiki/CoovaFX">CoovaFX version 1.3</a>. Right click on the (enabled) Coova icon selecting <span style="font-style: italic">Launch CoovaEWT</span> under the <span style="font-style: italic">Config</span> menu. This will bring up the embedded web application, ready for you to enter the IP Address of the CoovaEWT enabled device.

[img_assist|nid=181|title=|desc=|link=none|align=center|width=450|height=306]

Of course, you will need to have a CoovaEWT enabled device before this application is usable, see below.

Also in the version 1.3 release is the ability to change the User-Agent used in WISPr requests.

<strong>Open-mesh w/ EWT</strong>

While doing a bit of work on open-mesh routers, I found it nice to have at least a minimal user interface. If for nothing else, to check status information and start and stop chilli.

[img_assist|nid=182|title=|desc=|link=none|align=center|width=499|height=337]

<a href="/wiki/CoovaEWT/OpenMesh">Download and install capd-open-mesh</a>.

<strong>OpenWrt w/ EWT</strong>

Very much a work in progress, but enough to play with and get started using. Backup your UCI settings before using. After making changes, be sure to verify your UCI settings.

[img_assist|nid=183|title=|desc=|link=none|align=center|width=500|height=320]

<a href="/wiki/CoovaEWT/OpenWrt">Download and install capd-openwrt</a>.

<strong>Road to CoovaAP 2.0</strong>

Many people have been asking about a new release for <a href="/wiki/CoovaAP">CoovaAP</a>. While there are some bugs, it still remains probably the best, most integrated, open-source Hotspot-centric firmware available. The difficult issue going forward is that the current version is based on OpenWrt WhiteRussian which is no longer supported, even in the slightest, by OpenWrt. Upgrading to Kamikaze is the right thing to do, however, it brings other complications - like the lack of nvram, a completely new configuration system, and a wider range of hardware and software to support. For CoovaAP 2.0, the Kamikaze version, the idea is to use CoovaEWT for the web interface and package everything for easy installation on stock OpenWrt devices, using the standard software repositories.

However, with <a target="_blank" href="http://www.mail-archive.com/openwrt-devel@lists.openwrt.org/msg01710.html">X-Wrt, Lua, and LuCI being more integrated into the stock OpenWRT distribution</a>, it may become problematic as I foresee configuration and init script differences and conflicts. While X-Wrt tries to make everything (but the kitchen sink) configurable for <span style="font-style: italic">software</span> <span style="font-style: italic">application</span>, CoovaAP is kept simple and integrated across applications to configure for <span style="font-style: italic">firmware</span> <span style="font-style: italic">features</span>. The X-Wrt project is moving in the direction of being more integrated, driven by the features presented in their web interface. But, with their <span style="font-style: italic">feature</span> configuration logic tied to their web interface (and dependencies), it is unlikely that we can combine efforts. In my opinion, OpenWrt would be better off abstracting the <span style="font-style: italic">feature</span> configuration logic into an API (which could be UCI itself) separate from their web presentation. If they did this, I believe it would broaden the development community and better the project by not limiting the <span style="font-style: italic">feature set</span> to that of one web interface.

In the end, we will probably have to distribute pre-built images for CoovaAP 2.0 set to use our own repositories. With no 'upgrade path' between WhiteRussian and Kamikaze, it would be nice to keep supporting the CoovaAP 1.X branch - for this we ask for community involvement and support!
