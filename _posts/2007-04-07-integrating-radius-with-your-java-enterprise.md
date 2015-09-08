---
status: old
layout: post
title: Integrating RADIUS with your Java Enterprise
created: 1175971108
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
<a href="/JRadius">JRadius</a> is a project I started to not only address the need for a Java RADIUS client capable of EAP-based authentication, but for a Java framework for processing RADIUS authentication and accounting through a server front end like <a href="http://freeradius.org/">FreeRADIUS</a>. Why? Well, for several reasons. First, I primarily had Java programmers. But, also because Java offers a lot in terms of portability and integration with other Java components and systems. This article will help point you in the right direction to get up and running with JRadius in both the client and server context - there will be more articles and wiki documentation to come.

<strong>Using JRadius with FreeRADIUS</strong>

The first thing you need is a FreeRADIUS server with the JRadius module. Instructions on how to do this are <a href="/JRadius/FreeRADIUS">here, in the wiki</a>. The JRadius module, <em>rlm_jradius</em>, is what links the FreeRADIUS server to the JRadius server. Using pooled connections, requests are taken out of FreeRADIUS and passed on to JRadius for processing. The basic structure of a JRadius handler looks like:
<pre class="code">
<div>public class MyHandler extends PacketHandlerBase {</div>
<div style="padding-left: 2em">public boolean handle(JRadiusRequest request) {
<div style="padding-left: 2em">AttributeList ci = request.getConfigItems();
RadiusPacket req = request.getRequestPacket();
RadiusPacket rep = request.getReplyPacket();</div>
<div style="padding-left: 2em">String u = (String)req.getAttributeValue(Attr_UserName.TYPE);</div>
<div style="padding-left: 2em">...</div>
</div>
<div style="padding-left: 2em">}</div>
<div>}</div>
</pre>
From within the JRadius Java server, you are able to do just about everything any other FreeRADIUS module can do. This includes adding, removing, or altering attributes in the request, the reply, or the internal FreeRADIUS "config items" attribute list. The latter is used within FreeRADIUS - often using FreeRADIUS internal only attributes - to control the state and behavior of the request.
<pre>AttributeList ci = request.getConfigItems();
ci.add(new Attr_UserPassword("password"));</pre>
For instance, to give FreeRADIUS the plain text password of a user (to be used by FreeRADIUS during actual authentication), you might have the above in your <em>authorize</em> JRadius handler.

<strong>Running JRadius Server</strong>

To get your handlers up and running, you need a JRadius server. Instructions on how to build and get an example server running is <a href="/JRadius/RunServer">found in the wiki</a>. You can easily build from the <a href="http://dev.coova.org/svn/cjradius/">JRadius SVN</a> using Maven and Ant. Doing <em>mvn install</em> will setup the dependencies and create jar files in the typical <em>target</em> directory for <em>core</em> (core JRadius client and server), <em>dictionary</em> (attribute dictionary), <em>extended</em> (JRadius classes that require the dictionary), and <em>example</em> (a couple examples). Using Ant by doing <em>ant dist</em> will create just 2 jars in the <em>dist</em> directory - <em>jradius.jar</em> and <em>jradius-dictionary.jar</em>, where the former contains everything minus the dictionary. To summarize the steps in getting the JRadius example server running:
<pre>svn co http://dev.coova.org/svn/cjradius/
cd cjradius
ant dist
ant run-example</pre>
You can find the example source code in the <a href="http://dev.coova.org/svn/cjradius/java/example/org/jradius/example/"><em>java/example</em></a> directory which can be extended to suite your specific needs.

<strong>Using JRadius Client </strong>

<a href="/wiki/JRadius_ClientAPI">The Client API</a> is simple and able to do a variety of authentication protocols - including PAP, MSCHAPv2, EAP-MD5, and EAP-TTLS/PAP. JRadius can be integrated into any Java authentication scheme. For instance, it has been used with Jive Wildfire and <a href="http://rags.6pack.org/doku.php">Shibboleth</a>.

<strong>Development and Support </strong>

For questions, suggestions, bug reports, patches, and the like; I have created a <a href="/forum/">JRadius Forum</a>.
