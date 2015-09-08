---
status: old
layout: post
title: CoovaChilli on Ubiquiti
created: 1258723894
categories:
- !binary |-
  YXBwbGljYXRpb25z
---
In the forum and elsewhere, we have seen people asking for [for their [http://www.ubnt.com/ Ubiquiti](CoovaChilli](/CoovaChilli)) routers. Of course, one easy way to use [is to be using the [http://dev.open-mesh.com/ open-mesh / ROBIN firmware](CoovaChilli](/CoovaChilli)). Another way is to build [right into the Ubiquiti firmware using the [http://www.ubnt.com/support/sdk.php Ubiquiti AirOS SDK](CoovaChilli](/CoovaChilli)).

*Jan 16 2010: Updated for CoovaChilli 1.2.1 (rev 281)*

== Building [into the [http://www.ubnt.com/support/sdk.php AirOS SDK](CoovaChilli](/CoovaChilli)) ==

The [Ubiquiti AirOS SDK](http://www.ubnt.com/wiki/index.php/AirOS-SDK) lets you make changes to the standard Ubiquiti firmware. Here is how to add CoovaChilli and the embedded captive portal. Follow the [directions from Ubiquiti](http://www.ubnt.com/wiki/index.php/Setting_up_build_environment_in_Ubuntu_for_re-compiling_AirOS) on how to setup the SDK on Ubuntu.

In this example, we will be building and installing the latest [CoovaChilli from subversion](http://www.coova.org/CoovaChilli/Developers). We have been busy with CoovaChilli, wanted to get those changes in, and also we added [some files](http://dev.coova.org/svn/coova-chilli/distro/ubnt/) to make it easier to build in AirOS SDK.

Before proceeding, be sure you are familiar with how to upgrade the Ubiquiti router firmware and the [firmware recovery procedure](http://www.ubnt.com/wiki/index.php/Firmware_Recovery).

== Adding Packages ==

Once you have the necessary toolchain installed and have downloaded the SDK, go into the SDK directory (we are using version [SDK.UBNT.v3.5.4499](http://www.ubnt.com/downloads/firmwares/XS-fw/v3.5/SDK.UBNT.v3.5.4499.tar.bz2)).

 cd /path/to/SDK.UBNT.v3.5.4499/

Install the necessary source code and build files. In this case, we link to an existing CoovaChilli source directory (see [here](http://www.coova.org/CoovaChilli/Developers)) and we download haserl for the [embedded miniportal](http://www.coova.org/CoovaChilli/Miniportal).

 cd apps/gpl
 ln -s /path/to/svn/coova-chilli coova-chilli
 ln -s coova-chilli/distro/ubnt/coova-chilli.mk .
 ln -s coova-chilli/distro/ubnt/haserl.mk .
 wget http://downloads.sourceforge.net/project/haserl/haserl-devel/0.9.26/haserl-0.9.26.tar.gz
 tar xzf haserl-0.9.26.tar.gz
 mv haserl-0.9.26 haserl
 cd -

== Apply Patches ==

Now, we configure the xs2 target with CoovaChilli by apply the patch:

 patch -p1 < apps/gpl/coova-chilli/distro/ubnt/xs2.patch

The above patch will do several things, including:

* Enables a couple options in busybox (tr, head, basename, dirname, etc)
* Enables the tun/tap kernel module to be built as a module
* Enables the coova-chilli and haserl apps/gpl packages
* Tries to configure chilli to start on boot-up

To patch the Ubiquiti web interface for simple CoovaChilli configurations, apply the patch:

 patch -p1 < apps/gpl/coova-chilli/distro/ubnt/apps.web.patch

== Building ==

Build the new firmware:

 PATH=$PATH:. make clean xs2

If everything goes well, you should have the binary firmware, as shown here:

 $ ls  rootfs/XS2.ar2316.v3.5.latest/XS*.bin
 rootfs/XS2.ar2316.v3.5.latest/XS2.ar2316.v3.5.SDK.100122.0850-8M.bin
 rootfs/XS2.ar2316.v3.5.latest/XS2.ar2316.v3.5.SDK.100122.0850.bin

In our example we are using a Bullet2, so we used the [XS2.ar2316.v3.5.SDK.100122.0850.bin](http://ap.coova.org/ubnt/SDK.UBNT.v3.5.4499/XS2.ar2316.v3.5.SDK.100122.0850.bin) file.

* [Download XS2.ar2316.v3.5.SDK.100122.0850.bin](http://ap.coova.org/ubnt/SDK.UBNT.v3.5.4499/XS2.ar2316.v3.5.SDK.100122.0850.bin)
* [Download XS2.ar2316.v3.5.SDK.100122.0850-8M.bin](http://ap.coova.org/ubnt/SDK.UBNT.v3.5.4499/XS2.ar2316.v3.5.SDK.100122.0850-8M.bin)

== Installing ==

Install the firmware under the *System* tab:

[img_assist|nid=3675|title=|desc=|link=none|align=center|width=566|height=475]

Click on  **Upgrade** to have a file selection window appear. Find and select the AirOS firmware .bin file. Proceed to upgrade your router, being CAREFUL NOT TO UNPLUG YOUR ROUTER OR DISTURB THE UPGRADE IN ANY WAY. When done, will will find new options under the *Services* tab.

== Configuring ==

Basic required configurations:

* Under the *Link Setup* tab, set the *Wireless Mode* to be **Access Point**. Save any apply the changes.
* Under the *Network* tab, ensure your WAN is configured correctly and the router has DNS services.
* Under the *Services* tab, configure basic CoovaChilli settings.

To demonstrate the CoovaChilli settings, we have configured our router to be use with [CoovaNET](https://www.coova.net/). In our CoovaNET account, under the *Account* tab on the *My network* page we find the information we need. Essentially, you need to know the RADIUS server, RADIUS shared secret, RADIUS Administrator-User username and password, and the UAM Server URL.

[img_assist|nid=3677|title=|desc=|link=none|align=center|width=566|height=475]

Once your settings are entered, save the changes. You will see that when the Hotspot is configured to be active, the configuration page changes a bit to show a rudimentary status page.

[img_assist|nid=3679|title=|desc=|link=none|align=center|width=566|height=475]

To go back to the Hotspot settings, click on **Setup** and they will re-appear. You can toggle back and forth to the configuration settings, start and stop the service, and see the basic status information from this page.

[img_assist|nid=3681|title=|desc=|link=none|align=center|width=600|height=357]

Need to restore your firmware? You can get an original firmware here: http://www.ubnt.com/support/downloads.php

Need to recover the hard way? Follow the [Firmware Recovery](http://www.ubnt.com/wiki/index.php/Firmware_Recovery) directions. You might also find **CoovaFlash** (shown below) from the [CoovaFX](http://www.coova.com/CoovaFX) Firefox plug-in (shown in browser above) to help with the TFTP flashing. **Note:** Only TFTP an original firmware, even though we show otherwise in the screen shot.

[img_assist|nid=3683|title=|desc=|link=none|align=center|width=516|height=294]

We hope this helps you to get up and running with CoovaChilli on your Ubiquiti gear!
