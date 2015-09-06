---
layout: page
title: CoovaChilli with WPA Captive Portal
permalink: /CoovaChilli/WPACaptivePortal/
---

This page describes how [CoovaChilli](/CoovaChilli) can be used as a proxy for WPA 
authentication with the following twist:

- a user presenting valid credentials get on-line without restriction while
- a user presenting in-valid credentials will still gain WPA access, but be subject to a captive portal and walled garden.
- There are many ways to implement what is described here. For this example, however, we are using CoovaAP combined with FreeRADIUS and JRadius. You will also find this feature in the CoovaAAA services.

CoovaChilli
===========

To enable this feature within chilli itself, an option was defined. By setting the configuration flag wpaguests (in combination with the proxylisten, proxyport, and proxysecret settings) chilli will do a couple things:

sends a ChilliSpot-Config = allow-wpa-guests in proxy RADIUS Access-Request and
looks for ChilliSpot-Config = require-uam-auth in the Access-Accept reply such that
if not found, the access-accept is passed on normally giving the user full access;
if found, the access-accept is passed on, but the session is not marked as authenticated and is subject to ChilliSpots walled garden.
If the reply is an Access-Reject, then, of course, that is sent on by proxy and WPA is not granted.

FreeRADIUS
==========

Actual authentication of the WPA RADIUS is handled by FreeRADIUS. It must be configured for EAP, TLS, and PEAP. Additionally, this example uses the JRadius module to easily code our GuestWPA RADIUS logic.

For basics on FreeRADIUS and EAP authentication, see:

- Securing Your WLAN with WPA and FreeRADIUS, Part I
- Securing Your WLAN with WPA and FreeRADIUS, Part II
- 802.1X Port-Based Authentication HOWTO

JRadius
=======

For information on installing and using JRadius with FreeRADIUS, see:

- JRadius - Architecture
- JRadius - Building for FreeRADIUS
- JRadius - Getting started
- JRadius - Developer notes

For this example, the following JRadius handler is defined (abbreviated for readability):

    public class WPACaptivePortal extends PacketHandlerBase 
    {
       public boolean handle(JRadiusRequest request)
       {
           try
           {
               /*
                * Gather some information about the JRadius request
                */
               AttributeList ci = request.getConfigItems();
               RadiusPacket req = request.getRequestPacket();
               RadiusPacket rep = request.getReplyPacket();
 
               /*
                * Find the username in the request packet
                */
               String username = (String)req.getAttributeValue(Attr_UserName.TYPE);
 
               if (rep instanceof AccessAccept)
               {
                   RadiusLog.info(Allowing WPA access for username:  + username);
               }
               else
               {   // Is an Access-Reject
                   if (allow-wpa-guests.
                        equals((String)req.getAttributeValue(Attr_ChilliSpotConfig.TYPE))) 
                   {   // Allowing WPA guest access
                       if (req.findAttribute(Attr_EAPMessage.TYPE) != null)
                       {   // Is EAP (802.1x)
                           if (req.findAttribute(Attr_FreeRADIUSProxiedTo.TYPE) != null)
                           {   // Is the inner request, TLS termianted
                               rep = new AccessAccept();
                               rep.addAttribute(new Attr_ChilliSpotConfig(require-uam-auth));
                               request.setReplyPacket(rep);
 
                               ci.add(new Attr_AuthType(Accept));
                               request.setReturnValue(JRadiusServer.RLM_MODULE_UPDATED);
 
                               RadiusLog.error(Allowing Guest WPA access for username:  + username);
                               return true;
                           }
                       }
                   }
                   RadiusLog.info(Authentication failed for username:  + username);
               }
           }
           catch (RadiusException e) { e.printStackTrace(); }
         
           request.setReturnValue(JRadiusServer.RLM_MODULE_UPDATED);
           return false;
       }
    }

This handler is to be ran in the post-auth section of FreeRADIUS, as defined in this JRadius config.xml snippit:

    <chain name=post_auth>
       <init-session       name=post_auth-init-session
                           description=Initialize The Radius Session/>
 
       <command            className=org.coova.jradius.example.WPACaptivePortal />
 
       <class-post-auth    name=post_auth-class
                           description=Post-Auth Class Attribute Handler/>
    </chain>

And requires that FreeRADIUS is configured such that Access-Rejects are processed in the post-auth section too (by default, they are not):

     # in radiusd.conf
     post-auth {
        jradius
        Post-Auth-Type REJECT {
                jradius
        }
     }

CoovaAP Example
===============

Putting it all together, with a (FreeRADIUS/JRadius) RADIUS server up and running, the setup is tested using a Linksys running the CoovaAP firmware (version beta.4 or better).

On the HotSpot / RADIUS configuration page in the firmware, you can select to allow/enable WPA Guests.

It is important that chilli is started after everything else because it will actually rewrite some configurations (so that the nas program uses chillispot for RADIUS) and restarts other programs.

Some tests
Some simple tests using Mac OS X as the client (PEAP).

Example User Login
Just using a FreeRADIUS raddb/users entry to define the user:

    david   User-Password == testing
            WISPr-Redirection-URL = http://coova.org/

The user experience, at least on Mac OS X, is summarized by:
Found the SSID and was asked for a username, password, and 802.1x authentication type.
I entered my valid credentials leaving the auth type on Automatic.
I had to acknowledge the SSL (TLS) certificate because it is self signed ;)
I was logged in and able to browse the Internet
FreeRADIUS/JRadius log (highlights only):

    Access-Request packet from host 192.168.100.200:2084, id=2, length=170
        User-Name = david
        EAP-Message = 0x020200061900
        ChilliSpot-Config = allow-wpa-guests
        Calling-Station-Id = 00-11-24-90-XX-XX
        Called-Station-Id = 00-06-25-C5-XX-XX
        NAS-Port-Type = Wireless-802.11
        NAS-Port = 1
        NAS-IP-Address = 192.168.100.200
        NAS-Identifier = 00:06:25:c6:xx:xx
 
        .. EAP Access Challenge/Request and TLS Termination ..
  
    Sending Access-Accept of id 8 to 192.168.100.200 port 2084
        User-Name = david
        MS-MPPE-Recv-Key = 0x239ae8a15596cc224f6990e0713e3524dcac4cc22de68226d2de01fee7b4e77f
        MS-MPPE-Send-Key = 0x938b61d3487a87a6e1a2442767cd6c10036384f6b368d23e553ab53caf13e742
        EAP-Message = 0x03080004

Example Guest Login
-------------------

This time, I did the following:

- Found the SSID and connected to it
- When asked for username and password, I just put in anything
- I still had to acknowledge the SSL (TLS) certificate because it is self signed
- Got onto the WPA network, but got the captive portal page when trying to browse the Internet

FreeRADIUS/JRadius log (highlights only):

     Access-Request packet from host 192.168.100.200:2084, id=14, length=171
        User-Name = nobody
        EAP-Message = 0x020200061900
        ChilliSpot-Config = allow-wpa-guests
        Calling-Station-Id = 00-11-24-90-XX-XX
        Called-Station-Id = 00-06-25-C5-XX-XX
        NAS-Port-Type = Wireless-802.11
        NAS-Port = 1
        NAS-IP-Address = 192.168.100.200
        NAS-Identifier = 00:06:25:c6:xx:xx
 
        .. EAP Access Challenge/Request and TLS Termination ..
 
     Sending Access-Accept of id 19 to 192.168.100.200 port 2084
        ChilliSpot-Config := require-uam-auth
        MS-MPPE-Recv-Key = 0x317f2c50e739bd69d14be1d09ec111abe3f562886879b70eee16395637dc5eb5
        MS-MPPE-Send-Key = 0xcbc74e30dce41c343b4afe0ea90b7a6413b659bba3a330bcd265da9df4e85ae7
        EAP-Message = 0x03070004
        User-Name = nobody
