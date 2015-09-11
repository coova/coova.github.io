---
layout: page
menu: main
title: JRadius - Simulator
page_title: JRadius Simulator
permalink: /JRadius/Simulator/
---

Based on [JRadius](/JRadius) and Java Swing, the JRadiusSimulator is an open-source
stand-alone application designed to test RADIUS application and interconnections
by simulating RADIUS traffic. The application uses the JRadius Client API and
the generated JRadius Attributes Dictionary to make building and running RADIUS
simulations easy.

What it does
------------

JRadiusSimulator allows you to:

- use a graphical user interface for building and sending RADIUS packets;
- create a policy defining which attributes to send, in what type of packet, and what values to use;
- for RADIUS attributes with pre-defined values, provides a drop-down menu for ease of use;
- use multiple authentication methods including PAP, CHAP, MSCHAPv2, EAP-MD5, EAP-TLS, PEAP, and EAP-TTLS/PAP;
- easily verify RADIUS traffic against standards such as Intel's IRAP; and
- load and save configurations to better organize simulation configurations.

Getting Started
---------------

Run JRadiusSimulator Now!

The above URL is the easiest way to launch JRadiusSimulator provided your system
has Java Web Start (but is an older version of JRadius currently). Most current
operating systems now support Web Start. See the Java Web Start website for more
information.

JRadiusSimualtor can also be launched from the current JRadius release or
SVN. The main method is found in class net.jradius.client.gui.JRadiusSimulator
and a shell script simulator.sh is found in the release zip files to launch the
program.

    unzip jradius-client-1.1.4-release.zip
    cd jradius
    sh simulator.sh

Screen-shots
------------

![Screenshot 1](/img/JRSimulator1.jpg)

![Screenshot 2](/img/JRSimulator2.jpg)

![Screenshot 3](/img/JRSimulator3.jpg)

![Screenshot 4](/img/JRSimulator4.jpg)

![Screenshot 5](/img/JRSimulator5.jpg)
