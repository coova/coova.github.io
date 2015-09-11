---
layout: page
title: JRadius - Running JRadius Server
page_title: Running JRadius Server
permalink: /JRadius/RunServer/
---

JRadius works in conjuntion with FreeRADIUS, so you should already have your
FreeRADIUS installation setup for JRadius.

From Source
-----------

A good way to up and running with handler development is to download and build
using the current svn version. It can be used with Eclipse, ant, and maven.

Download Source
---------------

    git clone https://github.com/coova/jradius.git

Building Library and Dictionary
-------------------------------

Maven is used to build the JRadius project. Simply do:

    mvn clean install

Run Server
----------

Out of the box, JRadius doesn't really do that much. It is designed such that
you can easily write your own handlers to perform your RADIUS logic. To get
started, download and get the sample JRadius server running:

    unzip jradius-server-1.0.0-release.zip
    cd jradius
    sh start.sh
  
