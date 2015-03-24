---
layout: post
title: Embedding GWT - A new kind of web console
created: 1173785321
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
During the past few months, I have been doing a lot of work with the <a title="GWT" href="http://code.google.com/webtoolkit/">Google Web Toolkit</a> - an open-source Java software development framework that makes writing AJAX applications a bit easier. With GWT, you build your browser-based (client) application in Java which is "compiled" into a cross-browser JavaScript application.

GWT uses remote procedure calls (RPC) to pass data to and from the web server. Typically, the RPC calls are handled by a server-side Java application tightly integrated with the GWT application -- passing serialized Java objects back and forth. However, in this case, we are not using any Java inside the device. Instead, the server-side RPC is implemented as a CGI in C and passes data in the form of <a title="JSON" href="http://json.org/">JSON objects</a>.

Advantages to using GWT in devices:
<ul>
	<li>No resources wasted spawning scripts or formatting HTML for each page</li>
	<li>Data passed to and from device via well-formed JSON-RPC only</li>
	<li>Lightweight - shifting the workload to the browser instead of the device</li>
	<li>More secure than using shell scripts and parsing query string input</li>
</ul>
Perhaps one of the only drawbacks is the size of the GWT produced content. Uncompressed, an application of about 1300 lines of Java code compiles to a size of more than half a megabyte. When compressed, this goes down to around 250K. For some devices, this could be a show stopper. The GWT application is just static content, but the application must be downloaded from the same source as the RPC callbacks to work in a browser. Though, what about a desktop application? Looking forward to the <a title="Adobe Apollo" href="http://labs.adobe.com/wiki/index.php/Apollo">Adobe Apollo</a> project to see if the same GWT content can be dropped into a desktop application while still interfacing with and configuring devices using JSON-RPC.
