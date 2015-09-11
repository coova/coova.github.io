---
layout: page
title: JRadius - JRadius with RadSec
page_title: JRadius with RadSec
permalink: /JRadius/RadSec/
---

[JRadius](/JRadius) now has support for RadSec in both the client and server.

RadSec Client
=============

The RadiusClient class now can be configured with your own transport layer,
implementing the RadiusClientTransport abstract class. The default transport
class is UDPClientTransport, with the RadSecClientTransport being another
option.

RadSec in JRadiusSimulator
==========================

The JRadiusSimulator now has an option to pick either the UDP or RadSec
transport, allowing you to test both UDP and RadSec RADIUS servers. To configure
RadSec in the Simulator:

- Select **RadSec** from the **Transport** list on the main screen.
- For **RADIUS Server**, enter in your RadSec server IP address or hostname.
- Enter in the **Shared Secret** for use in the tunnel, *radsec* for instance.
- Enter the RadSec port in both **Auth Port** and **Acct Port**, port 2083 is the default RadSec port.
- Select the **Keys** tab and configure your X509 certificate and CA.

Using RadSec with the Client API
================================

When using UDP, a RadiusClient can be created in the same way as
before. However, when creating a client for RadSec, you must configure the
RadSecClientTransport, specifying the KeyManager and TrustManager to be used.

    RadiusClientTransport transport;
    transport = new RadSecClientTransport(keyManagers, trustManagers);
 
    transport.setRemoteInetAddress(InetAddress.getByName(radiusServer));
    transport.setSharedSecret(sharedSecret);
    transport.setAuthPort(authPort);
    transport.setAcctPort(acctPort);
    transport.setSocketTimeout(timeout);
 
    RadiusClient radiusClient = new RadiusClient(transport);
   
Now the radiusClient can be used.

RadSec Server
=============

The JRadius server is a RADIUS logic processing engine in Java. Typically, the
JRadius server is used with FreeRADIUS and the rlm_jradius module, allowing you
to use FreeRADIUS while processing your RADIUS logic in the JRadius Java
server. However, JRadius now is able to handle native RADIUS packets, not just
those coming through FreeRADIUS.

In our example, we will configure a RadSec listener and processors configured
with a simple KeyManager and TrustManager that use PEM encoded X509
certificates. We then will configure a very simple proxy handler that will
forward the RADIUS packets to an external RADIUS server.

To configure the JRadius server with a RadSec listener, you will have the
following in jradius-config.xml:

    <listener name="RadSecServices">
      <description>RadSec Listener</description>
      <class>bean:radSecListener</class>
      <processor-class>bean:radSecProcessor</processor-class>
      <processor-threads>6</processor-threads>
      <property name="backlog" value="1024"/>
      <property name="keyManager" value="bean:radSecKeyManager"/>
      <property name="trustManager" value="bean:radSecTrustManager"/>
      <packet-handler name="RadSec Proxy">
        <description>RadSec Proxy</description>
        <class>bean:radSecProxyHandler</class>
      </packet-handler>
    </listener>
In the above, we setup the RadSec listener and processor classes. In this case, the classes are created in the Spring Framework and we refer to the beans by name. The listener bean is radSecListener, the processor bean is radSecProcessor, and it is configured with a KeyManager, a TrustManager, and a packet handler class.

The beans above are defined and configured in the spring-config.xml file:

    <bean id="radSecProcessor" class="net.jradius.radsec.RadSecProcessor" singleton="false">
    </bean>
 
    <bean id="radSecListener" class="net.jradius.radsec.RadSecListener">
    </bean>
 
    <bean id="radSecKeyManager" class="net.jradius.radsec.SimpleKeyManager">
      <property name="keyFile" value="/tmp/server.pem"/>
      <property name="keyFileType" value="PEM"/>
      <property name="keyFilePassword" value="test"/>
    </bean>
 
    <bean id="radSecTrustManager" class="net.jradius.radsec.SimpleTrustManager">
      <property name="certFile" value="/tmp/ca.pem"/>
      <property name="certFileType" value="PEM"/>
      <property name="certFilePassword" value=""/>
    </bean>
 
    <bean id="radSecProxyHandler" class="net.jradius.radsec.SimpleProxyHandler">
      <property name="radiusServer" value="localhost"/>
      <property name="sharedSecret" value="testing123"/>
      <property name="authPort" value="1645"/>
      <property name="acctPort" value="1646"/>
    </bean>

In this example, we are using the simple RadSecListener and RadSecProcessor
classes to create the RadSec service. It is configured with a SimpleKeyManager
and a SimpleTrustManager to define the server X509 certificate and CA trust
chain. Then, finally, the SimpleProxyHandler is configured in this example to
forward RADIUS packets as UDP to a remote RADIUS server.

Simple Proxy Handler
====================

In our example, we configured the RadSec listener to use a simple proxy handler. Of course, you can configure the listener to use any handler or handler chain. In this case, the JRadius handler is simple:

    public boolean handle(JRadiusRequest request) throws Exception
    {
       RadiusRequest req = (RadiusRequest) request.getRequestPacket();
       RadiusResponse res = radiusClient.sendReceive(req, 3);
       request.setReplyPacket(res);
       return false;
    }

All it does is forward the RADIUS packet through to the configured RadiusClient
and stores the reply to be returned by the RadSec processor.

Notes
=====

Other implementations of RadSec:

- CoovaChilli RadSec
- RadSecProxy
- Radiator
