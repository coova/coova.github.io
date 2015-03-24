---
layout: post
title: Embedded Web 2.0
created: 1178197052
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
In a <a href="/node/60">previous post</a>, the idea of using the <a href="http://code.google.com/webtoolkit/">Google Web Toolkit</a> to create a new kind of embedded web administration interface for devices was discussed. I continue the discussion by providing some examples and a working demonstration of the user interface.

The interface is designed, in this case, to be the administrative web console of a <a href="http://openwrt.org/">OpenWrt</a>-based firmware. As such, it is a tool to configure (linux) system parameters and files - which may be different depending on the underlying system. For instance, the <em>WhiteRussian</em> branch of OpenWrt use <a href="http://wiki.openwrt.org/OpenWrtNVRAM">NVRAM</a> settings while <em>Kamikaze</em> uses the new <a href="http://wiki.openwrt.org/OpenWrtDocs/KamikazeConfiguration">UCI Configuration</a>.

<strong>Working with XML</strong>

The application in this example uses XML to define the system configuration and also to define the user interface to edit this configuration.  XML is well suited for this purpose and offers many benefits, including:
<ul>
	<li>Easy to read and edit by hand</li>
	<li>System independence and interoperability</li>
	<li>Transformed into other formats using a structured language</li>
	<li>Excellent open-source libraries, tools, and resources</li>
</ul>
The well-formed structure of the XML resources are converted into <a href="http://www.json.org/">JSON</a> objects by a CGI program running the server-side of the application. The GWT interface exchanges JSON objects with this CGI back-end to load or save data.

<strong>Defining system configuration</strong>

The GWT-based user interface is designed as a configuration editor. The configuration itself is stored in XML as specified in the <a href="http://ap.coova.org/xml/sysconfig.dtd">sysconfig DTD</a>. The DTD defines how a system is configured and is used for basic syntax verification. Here is a portion of the "config.xml" system configuration based on this specification:
<pre>&lt;sysconfig&gt;
&nbsp;&nbsp;&lt;system&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;settings&nbsp;boot_wait="true"&nbsp;hostname="Coova"/&gt;
&nbsp;&nbsp;&lt;/system&gt;
&nbsp;&nbsp;&lt;network&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;interface&nbsp;id="loopback"&nbsp;proto="static"&nbsp;.../&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;interface&nbsp;id="lan"&nbsp;proto="static"&nbsp;.../&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;interface&nbsp;id="wan"&nbsp;proto="dhcp"&nbsp;.../&gt;
&nbsp;&nbsp;&lt;/network&gt;
&nbsp;&nbsp;...
&lt;/sysconfig&gt;</pre>
The XML is transformed into JSON by the CGI program when sent to and stored by the GWT application (as a <a href="http://code.google.com/webtoolkit/documentation/com.google.gwt.json.client.JSONObject.html">JSONObject</a>), as shown in the "Status / Config Tree" tab of the demo.

<strong>Defining the user interface</strong>

The user interface screens are <a href="http://ap.coova.org/xml/ui.xml">defined in XML</a> based on the <a href="http://ap.coova.org/xml/cap-ui.dtd">cap-ui DTD</a>. The portion that builds the systems settings screen to configure the above XML segment is as follows:
<pre>&lt;cap-ui&gt;

&nbsp;&nbsp;&lt;menu&nbsp;name="System"&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&lt;submenu&nbsp;name="Settings"&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;inputset&nbsp;name="System&nbsp;Settings"&nbsp;object="system.settings"&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;input&nbsp;label="Host&nbsp;Name"&nbsp;key="hostname"&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/input&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;input&nbsp;label="boot_wait"&nbsp;key="boot_wait"&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;option&nbsp;name="Enabled"&nbsp;value="true"/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;option&nbsp;name="Disabled"&nbsp;value="false"/&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/input&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/inputset&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/submenu&gt;
&nbsp;&nbsp;&nbsp;&nbsp;...
&nbsp;&nbsp;&lt;/menu&gt;
&nbsp;&nbsp;...
&lt;/cap-ui&gt;</pre>
<strong>Configuration transformations</strong>

Taking the XML configuration and using it to set the underlying system configuration is done using <a href="http://www.w3.org/TR/xslt">XSLT</a>. Transforms take the XML and produce scripts for WhiteRussian (<a href="http://ap.coova.org/xml/xml2nvram.xsl">example</a>) and Kamikaze (<a href="http://ap.coova.org/xml/xml2uci.xsl">example</a>), the output of which is shown in the "Status / Config Files" tab of the demo.

<strong>The demo
</strong>

See an <a href="http://ap.coova.org/cgi-bin/ewt-cgi/com.coova.ewt.Home/Home.html">on-line demonstration</a> of the user interface using something similar to the above configuration. Please, keep in mind it is still a work in progress and not all the screens and dependencies are defined. The configurations transforms are also incomplete - as is the UCI configuration of Kamikaze.

If you want to help out, come join the <a href="/forum/">forum</a>! (when your done helping out <a href="https://dev.openwrt.org/">OpenWrt</a>) ;)
