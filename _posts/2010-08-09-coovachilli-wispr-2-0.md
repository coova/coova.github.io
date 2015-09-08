---
status: old
layout: post
title: CoovaChilli WISPr 2.0
created: 1281338462
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
---
The WISPr 1.0 document by the Wi-Fi Alliance set out to defined the
**Best Current Practices for Wireless Internet Service Provider
(WISP) Roaming** in an effort to bring some consistency to
authentication and billing on Wi-Fi Public Access Networks. While the
document does give some good guidance on the minimal RADIUS
requirements for AAA (Authentication, Authorization, and Accounting),
and defines a methodology for automated login in a captive portal
network, it was not designed to be a standard, so it says. The
document goes on to warn implementors that they may not claim to be
*Wi-Fi Alliance* or even *WISPr* compliant and the document
_may_ contain intellectual property belonging to a third party. It
says "users assume the full risk of using the document, including
the risk of infringement" and that "users are responsible for
securing all rights to any intellectual property herein from third
parties to whom such property may belong."

I've always considered it a bit strange to spell out industry _best practices_
that _may_ infringe on the rights of a third party, especially when
the third party in question is one of the authors.

Regardless, there is now a _WISPr 2.0_ specification being promoted
by the Wireless Broadband Alliance (WBA) which extends on the previous
version to hopefully reduce the number of interoperability issues and
to bring EAP authentication protocols (used in 802.1X) to the
browser-based Universal Access Method (UAM) captive portal.

CoovaChilli supports WISPr 2.0
------------------------------

We are pleased to announce that CoovaChilli will now support WISPr
2.0, in addition to 1.0, thanks to code contributions from
Comfone/WeRoam which we have merged into the CoovaChilli subversion
trunk. Comfone, by the way, also sponsored the original implementation
of WISPr 1.0 in Chillispot. Give thanks!

Here is a brief overview of a WISPr 2.0 login through CoovaChilli.

The WISPr 2.0 XML was expanded to include some additional
_MessageType_ and _ResponseCode_ values as well as the XML
elements _VersionHigh_, _VersionLow_, and the _EAPMsg_. Below is
an example initial redirect by CoovaChilli showing the WISPr 2.0
XML. (URLs are shortened with _..._ for readability.)

     GET / HTTP/1.1
     User-Agent: WISPR! Coova WISPr Client (Java: 1.6.0_21)
     Host: www.microsoft.com

     HTTP/1.0 302 Moved Temporarily
     Location: https://coova/www/login.chi?res=notyet&uamip=10.1.0.1&uamport=3990...
     Content-Type: text/html; charset=UTF-8
     Content-Length: 868
     Connection: close

     <HTML><BODY><H2>Browser error!</H2>Browser does not support redirects!</BODY>
     <!--
     <?xml version="1.0" encoding="UTF-8"?>
     <WISPAccessGatewayParam
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="http://www.wballiance.net/wispr_2_0.xsd">
     <Redirect>
     <MessageType>100</MessageType>
     <ResponseCode>0</ResponseCode>
     <VersionHigh>2.0</VersionHigh>
     <VersionLow>1.0</VersionLow>
     <AccessProcedure>1.0</AccessProcedure>
     <AccessLocation>CDATA[[isocc=,cc=,ac=,network=Coova,]]</AccessLocation>
     <LocationName>CDATA[[My_HotSpot]]</LocationName>
     <LoginURL>https://coova/www/login.chi?res=wispr&amp;uamip=10.1.0.1&amp;uamport=3990&amp;...</LoginURL>
     <AbortLoginURL>http://10.1.0.1:3990/abort</AbortLoginURL>
     <EAPMsg>AQEABQE=</EAPMsg>
     </Redirect>
     </WISPAccessGatewayParam>
     -->
     </HTML>

For comparison, here is a pure WISPr 1.0 XML block (CoovaChilli can be
told to only support 1.0 with the _--nowispr2_ option):

     <?xml version="1.0" encoding="UTF-8"?>
     <WISPAccessGatewayParam
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="http://www.wballiance.net/wispr_2_0.xsd">
     <Redirect>
     <MessageType>100</MessageType>
     <ResponseCode>0</ResponseCode>
     <AccessProcedure>1.0</AccessProcedure>
     <AccessLocation>isocc=,cc=,ac=,network=Coova,</AccessLocation>
     <LocationName>My_HotSpot</LocationName>
     <LoginURL>https://coova/www/login.chi?res=wispr&amp;...</LoginURL>
     <AbortLoginURL>http://10.1.0.1:3990/abort</AbortLoginURL>
     </Redirect>
     </WISPAccessGatewayParam>

Smart clients that don't support WISPr 2.0 shouldn't have an issue
with the extra XML elements. Clients that do support WISPr 2.0 can
detect what versions the access gateway supports and can choose which
to use. When using WISPr 2.0, the smart client picks up the _EAPMsg_
for processing before sending it's EAP response back to the login URL.

In the above example, we are using the CoovaChilli embedded
_miniportal_ captive portal, which is served up by CoovaChilli
itself (though, that isn't required). It is important that the WISPr
login URL points to an application that can handle both WISPr 1.0 and
2.0. To support WISPr 2.0, our login.chi script contains:

     if [ "$FORM_res" = "wispr" ] && [ "$FORM_WISPrEAPMsg" != "" ] && [ "$FORM_WISPrVersion" = "2.0" ] && {
         url="https://coova/login"
         http_redirect2 "$url?username=$FORM_username&WISPrEAPMsg=$FORM_WISPrEAPMsg&WISPrVersion=2.0"
     }

which simply redirects the request back to the CoovaChilli login
handler, as shown in the HTTP exchange below.

     GET /www/login.chi?res=wispr&...&UserName=test&WISPrEAPMsg=...&WISPrVersion=2.0 HTTP/1.1
     User-Agent: WISPR! Coova WISPr Client (Java: 1.6.0_21)
     Host: coova

     HTTP/1.1 302 Redirect
     Location: https://coova/login?username=test&WISPrEAPMsg=...&WISPrVersion=2.0
     Connection: close

CoovaChilli then handles the login request, taking the EAP-Message
send by the smart client and puts it into a RADIUS Access-Request that
is sent to the RADIUS server. When the RADIUS server replies with an
Access-Challenge and an EAP-Message response, CoovaChilli then bounces
the smart client back to the login handler with the EAP response
contained in the WISPr XML, as shown below.

     GET /login?username=test&WISPrEAPMsg=...&WISPrVersion=2.0 HTTP/1.1
     User-Agent: WISPR! Coova WISPr Client (Java: 1.6.0_21)
     Host: coova

     HTTP/1.0 302 Moved Temporarily
     Location: https://coova/www/login.chi?res=challenge&...
     Content-Type: text/html; charset=UTF-8
     Content-Length: 652
     Connection: close

     <HTML><BODY><H2>Browser error!</H2>Browser does not support redirects!</BODY>
     <!--
     <?xml version="1.0" encoding="UTF-8"?>
     <WISPAccessGatewayParam
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="http://www.wballiance.net/wispr_2_0.xsd">
     <EAPAuthenticationReply>
     <MessageType>121</MessageType>
     <ResponseCode>10</ResponseCode>
     <EAPMsg>AQIAFgQQLh0uQthjM0PZoQBHT6wE0Q==</EAPMsg>
     <LoginURL>http://coova/www/login.chi?res=wispr&amp;...</LoginURL>
     </EAPAuthenticationReply>
     </WISPAccessGatewayParam>
     -->
     </HTML>

The above loop continues until the EAP authentication is
complete. When CoovaChilli is given an Access-Reject or an
Access-Accept from the RADIUS server, the appropriate response is
given. Here is a successful login:

     GET /login?username=test&WISPrEAPMsg=...&WISPrVersion=2.0 HTTP/1.1
     User-Agent: WISPR! Coova WISPr Client (Java: 1.6.0_21)
     Host: coova

     HTTP/1.0 302 Moved Temporarily
     Location: https://coova/www/login.chi?res=success&...
     Content-Type: text/html; charset=UTF-8
     Content-Length: 646
     Connection: close

     <HTML><BODY><H2>Browser error!</H2>Browser does not support redirects!</BODY>
     <!--
     <?xml version="1.0" encoding="UTF-8"?>
     <WISPAccessGatewayParam
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="http://www.wballiance.net/wispr_2_0.xsd">
     <EAPAuthenticationReply>
     <MessageType>121</MessageType>
     <ResponseCode>50</ResponseCode>
     <EAPMsg>AwIABA==</EAPMsg>
     <LogoffURL>http://10.1.0.1:3990/logoff</LogoffURL>
     <StatusURL>http://10.1.0.1:3990/status</StatusURL>
     <MaxSessionTime>0</MaxSessionTime>
     <RedirectionURL></RedirectionURL>
     </EAPAuthenticationReply>
     </WISPAccessGatewayParam>
     -->
     </HTML>

In this example, we used EAP-MD5 and our own smart client based the
CoovaFX firefox add-on. For more information on supporting WISPr in
your network, [contact us](http://www.coova.org/contact).

References:

* [Comfone website](http://www.comfone.com/)
* [Wireless Broadband Alliance (WBA)](http://www.wballiance.net/)
* [WBA EAP over WISPr trial page](http://wballiance.net/WBA_EAPoverWISPr.html)
* [Article about WISPr 2.0](http://www.ispreview.co.uk/story/2010/06/21/wireless-broadband-alliance-makes-wifi-isp-roaming-easier-with-wispr-2.html)
* [Another article about WISPr 2.0](http://www.zdnet.co.uk/news/networking/2010/06/23/wispr-20-boosts-roaming-between-3g-and-wi-fi-40089325/)
* [Has link to original WISPr 1.0 PDF](http://blog.marcelotoledo.org/2007/12/27/wispr-spec-wireless-isp-roaming/)
* [Article about Nomadix patent(s)](http://wifinetnews.com/archives/2004/01/industry_expert_analyzes_nomadix_patent.html)
