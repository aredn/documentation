================
Beginner's Guide
================

*Contributor: Orv Beach W6BI*

What it’s all about
-------------------

By loading the AREDN |trade| firmware in a outdoor wireless access point, you can join a ham radio network. It’s like the Internet but runs on ham radio frequencies, mostly in the 2.4, 3.4, and 5.8 GHz bands. By joining this network you can find and use all sorts of applications (known as “services”). Anything running on a server, like weather stations, web sites showing site conditions, and email servers can be provided as a service. There are also services that don’t rely on a browser: video streams, chat servers, and VOIP PBXes. The network can also be used to connect Winlink stations, Dstar and DMR repeaters, and Allstar devices. Pretty much any kind of service you can put on the Internet you can put on the AREDN network, subject to the restrictions of the ham radio regulations (FCC “Part 97”).

RF access to the network
------------------------

How do you find out where the nearest network node is? There are several ways:

- Check the mesh map at arednmesh.org. If you don’t find one near your QTH, don’t despair; the map only shows a fraction of the nodes on the air. If you’re in any of these areas, there are realtime network maps that can help you determine if there’s a node in your area.

  - Central & Southern California: https://mapping.kg6wxc.net/meshmap
  - Yakima, WA: http://ka7hak.thatip.net:7773/meshmap
  - Oregon: https://arden.k9rcp.net/meshmap/map_display.php
  - San Franciso: https://sfmap.xojs.org/
  - Hawaii: http://42561.noip.us:8888/meshmap

- Create an account on arednmesh.org and see if there’s a Regional Forum for your area. Ask there for local information. If you don’t find a regional forum for your area, get it started by asking the webmaster, Randy WU2S, to create one for you. Search for his callsign using the search function, and by finding it you’ll be able to drop him a note. Once it’s created, create a post mentioning you’d like to get started and asking if there’s any activity near you.

- Ask around your local ham club or on a local net.

These network nodes behave very much like handie-talkies. That is, they’re low power and line of sight, so you typically end up talking to a network node on a hilltop, mountaintop, or some other elevated location (e.g. water tower).
So if you determine there is a local node, how do you find out if you can reach it?

For these devices, line of sight is REALLY line of sight; they don’t do trees well at all. There are a number of on-line LOS calculators, ranging from simple to use to really complex. A simple one is at https://heywhatsthat.com. By entering your location, expected elevation of your node, and naming it, the site will generate a coverage plot for you. You can do this for your QTH and/or any existing local nodes. (See the *Network Design Guide* for other tools.)

Alternate access to the network
+++++++++++++++++++++++++++++++

If after doing your research you find that you don’t have any RF path to the network, don’t despair; there is an alternative. The nodes have the capability of ‘tunneling’ over the Internet to another node. While this isn’t a radio connection, it will let you get on the network until such time as the network has grown into your area.

In order to establish a tunnel, you’ll need an additional piece of network equipment beyond the node itself. The current preferred device is the Mikrotik hAP AC Lite router which when running AREDN |trade| firmware will provide your node access to the Internet (plus a host of other really useful features when running a ham network in your shack). Current price on Amazon is about $50.

Recommended equipment
---------------------

The following recommendations are for a home station. Recommendations for network nodes on hilltops are likely to be different and beyond the scope of this introductory article. In order to ensure good performance you need a strong RF link to the network. Like most other ham radio activities, more gain is better than less. And even if you have two nodes within range the node’s routing software will always pick the strongest one as your path into the network. Omnidirectional antennas are discouraged and dish antennas greatly preferred.

All of the equipment using dish antennas supported by AREDN |trade| use electronics integrated into the feedpoint: two transceivers, two modems, and an embedded computer with RAM, ROM, and a network interface. They are all POE- enabled (Power Over Ethernet). This avoids having to run both a network cable and a power cable up a mast to the node. A web interface is used to control and configure the device.

Obviously your equipment will need to be on the same band as the node you want to connect to. If there are both 2 GHz and 5 GHz nodes equidistant from you with similar path characteristics, choose 5 GHz. That band is quieter, there’s more bandwidth, more channels, and the gear is about the same cost (and in some cases noticeably less).

Fortunately AREDN |trade| now supports dozens devices (including new ones added in the nightly builds), so there are many options when choosing what to buy. The Mikrotik dishes may be slightly less durable than equivalent Ubiquiti dishes, so if you live where there’s severe icing choose more rugged equipment. Reportedly the Mikrotik receivers may be slightly more sensitive than Ubiquiti, and Mikrotik dishes are lighter, making them more suitable for portable work (e.g., go boxes). But both brands work well.

Important considerations
++++++++++++++++++++++++

- The older models of equipment have less flash memory and RAM than current versions. The latest AREDN |trade| firmware runs on these devices but there are not enough resources to run services like tunnels. As time goes on the AREDN |trade| firmware grows slowly, so at some point in time it will no longer fit in the available resources of older devices. Don’t buy any used equipment unless you know it has at least 16 MB of flash and 64 MB of RAM and is “MIMO”. The AREDN |trade| team has flagged those devices that are no longer recommended for new purchase in the `Supported Platform Matrix: <https://www.arednmesh.org/content/supported-devices-0>`_.

Do not stand in front of the radio for extended periods of time when it’s powered on. NEVER look into the focus of the radio when it’s powered on. These small dishes have 80-100 watts of ERP at 5.8 Ghz! The Mikrotik Basebox 2 has 30 dBm of power output. When fed to a Mikrotik 30dB gain dish, that’s 1 KW of ERP. Use caution!




.. image:: _images/link-azimuth.png
   :alt:  Antenna Aiming Details
   :align: center

|
