---
layout: post
title: OS Fingerprinting
created: 1252681866
categories:
- !binary |-
  ZGV2ZWxvcG1lbnQ=
- !binary |-
  YXBwbGljYXRpb25z
---
In [[DHCP Discovery]], we explored the [http://www.faqs.org/rfcs/rfc2131.html DHCP protocol] and the kind of information the client device reveals about itself. [http://myweb.cableone.net/xnih/download/bh-japan-laporte-kollmann-v8.ppt DHCP fingerprinting] is taking that information in order to classify the operating system and/or vendor of the device. The technique is finding it's way into [http://meraki.com/blog/2009/09/10/os-fingerprinting/ commercial applications], [http://www.coova.com/CoovaRADIUS CoovaRADIUS] included, but, it's easy to do yourself too; here's how. 

== [[CoovaChilli]] ==

Enable the ''dhcpradius'' option to have CoovaChilli include some DHCP information in each MAC authentication triggered RADIUS Access-Request. 

[img_assist|nid=206|title=|desc=|link=none|align=center|width=585|height=257]

In this example, we are mostly interested in the DHCP ''Parameter Request List'' option which comes through in RADIUS as VSA ''ChilliSpot-DHCP-Parameter-Request-List''. 

== [[JRadius]] ==

To illustrate how to use the RADIUS attribute in the back-end, here is an example using [[JRadius]].

First, we can quickly parse out the [http://www.packetfence.org/en/tour/advanced_features.html PacketFence] DHCP [http://www.packetfence.org/dhcp_fingerprints.conf fingerprints file] into a HashMap:

  private HashMap<String, String> dhcpFingerprints = new HashMap<String, String>();
	
  public void loadDHCPFingerprints() throws Exception {
	URL url = new URL("http://www.packetfence.org/dhcp_fingerprints.conf");
	BufferedReader in = new BufferedReader(new InputStreamReader(url.openStream()));
	String line=null, desc=null;
	boolean fingers=false;
	
	while ((line = in.readLine()) != null) {
		if (line.startsWith("description=")) {
			desc = line.substring(12);
		}
		else if (line.startsWith("fingerprints=")) {
			fingers = true;
		}
		else if (fingers && line.startsWith("EOT")) {
			fingers = false;
		}
		else if (line.equals("")) {
			fingers = false;
			desc = null;
		}
		else if (fingers && desc != null) {
			String s[] = line.split(",");
			byte[] key = new byte[s.length];
			for (int i=0; i<key.length; i++)
				key[i] = (byte) Integer.parseInt(s[i]);
			String keyString = Hex.byteArrayToHexString(key);
			dhcpFingerprints.put(keyString, desc);
		}
	}
  }

We only need to do that once. Now, when processing our RADIUS request in JRadius, we can classify the client device:

  public String classifyClientDevice(RadiusPacket req) {
        byte[] parameterList = (byte[]) 
                  req.getAttributeValue(Attr_ChilliSpotDHCPParameterRequestList.TYPE);
        return dhcpFingerprints.get(Hex.byteArrayToHexString(parameterList));
  }

That's how you can do it in JRadius, but the same can be done in your preferred FreeRADIUS module. 