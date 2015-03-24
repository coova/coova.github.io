---
layout: post
title: Updates, Facebook Pages
created: 1195723057
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
There are new releases to announce, first of all. <a href="/CoovaChilli">CoovaChilli</a> version 1.0.11 was released with some bug fixes, leading to a new version of <a href="/CoovaAP">CoovaAP</a>, released as 1.0-beta.7d, to include the new Chilli. Last, but not least, <a href="/CoovaAAA">CoovaAAA</a> was updated, as was the <a href="http://www.facebook.com/apps/application.php?id=7108185615">Coova HotSpot</a> Facebook application, to work with the new <a href="http://www.facebook.com/business/?pages">Facebook Pages</a>. Now, you can use CoovaAAA along with either CoovaAP or CoovaChilli to authenticate Wi-Fi HoSpot visitors based on your Facebook Page fans!

<strong>Facebook Profile HotSpot</strong>

<a href="/node/96">As mentioned</a>, once you <a href="http://www.facebook.com/add.php?api_key=aad8b8add2c4dd0216292d644d25b203">add the Coova HotSpot application to your profile</a> you can then <a href="/CoovaAAA/Facebook">configure your Coova-enabled Wi-Fi HotSpot</a> to automatically allow you and your friends to reach the entire Internet - while all other visitors are only allowed access to the walled-garden. It's a great way to share your Wi-Fi with those you know and for those you don't know to introduce themselves. Introducing yourself first, after all, is the social thing to do, right?

<strong>Facebook Page HotSpot</strong>

<a href="http://www.facebook.com/business/?pages">Facebook introduced pages</a> that you can create for your restaurant, hotel, cafe, club, or just about any other business or organization. Instead of having Friends, like your Profile, Pages allow users to self-proclaim themselves as "Fans" - and gives the page owner a convenient way to communicate with their fan-based. The <a href="http://www.facebook.com/apps/application.php?id=7108185615">Coova HotSpot</a> application now supports Pages in addition to Profiles as being the "owner" of a HotSpot. Just like how the Profile HotSpot allows only you and your friends Internet access, the Page HotSpot will automatically login the Admins and Fans of the page. Follow the <a href="/CoovaAAA/Facebook">directions for setting up your HotSpot</a>, but use the "Page ID" instead of your "Profile ID" as the HotSpot owner.

<strong>How To Setup</strong>

The first step is always to <a href="http://www.facebook.com/add.php?api_key=aad8b8add2c4dd0216292d644d25b203">add the Coova HotSpot application to your profile</a>. You need this in your profile before you can setup or access a HotSpot using the application. Before setting up a HotSpot, you will also need to <a href="https://coova.org/app/c/signup.html">sign-up for a Coova account</a>. Link your Facebook profile to your Coova account by clicking on the Coova Hotspot application link on the left navigation bar in Facebook. Login to the embedded CoovaAAA manager once to link the accounts. The next time you visit the manager, you will be automatically logged into Coova.org.

Next, proceed to <a href="http://www.facebook.com/pages/create.php">create your page</a> and also <a href="http://www.facebook.com/add.php?api_key=aad8b8add2c4dd0216292d644d25b203&pages">add the Coova HotSpot application to the page</a>. Configure CoovaAP or CoovaChilli as <a href="/CoovaAAA/Facebook">described in the directions</a> using the Page ID as the HotSpot owner, as explained above, and your personal RADIUS shared secret from your Coova account. Oh, don't forget to publish your Facebook page!

When you have your page and HotSpot setup, connect to your HotSpot logging in to Facebook as an admin of the page. The first time you do this, you will be given instructions on how to link this page to your Coova account, as shown here:

[img_assist|nid=271|title=|desc=|link=none|align=center|width=516|height=373]

You'll notice that the example Facebook page used here was created with name "<a href="http://www.facebook.com/profile.php?id=5895514871">Cafe Wi-Fi</a>" and this Facebook user account is an Admin of the page (note: the "HotSpot Cafe Wi-Fi" title comes from the <em>Location Name</em> configured in the <em>HotSpot</em> / <em>Location</em> section of the CoovaAP admin interface). This Facebook user is already linked to a Coova account. After making sure the HotSpot is configured with that Coova account's RADIUS shared secret, link the page to your Coova account by clicking on <em>do this now!</em>. Then, with the HotSpot properly configured and linked to a Coova account, Admin users are automatically logged in:

[img_assist|nid=273|title=|desc=|link=none|align=center|width=516|height=373]

When a Facebook user, who is not a fan, tries to access the Internet, they will see:

[img_assist|nid=275|title=|desc=|link=none|align=center|width=516|height=373]

Where the links on the page will take the user to the <a href="http://www.facebook.com/profile.php?id=5895514871">Cafe Wi-Fi</a> Facebook page - where the user can sign-up as a Fan. Once they do, they will be able to get on-line:

[img_assist|nid=277|title=|desc=|link=none|align=center|width=516|height=373]

It's that simple! We will, of course, keep adding features... and suggestions are always welcome in the <a href="/forum/">forum</a>.
