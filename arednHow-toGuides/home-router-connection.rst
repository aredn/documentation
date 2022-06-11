================================
Connecting Nodes to Home Routers
================================

There are several indoor AREDN |trade| nodes that have more than one Ethernet port, including the *Mikrotik hAP ac lite* as well as the *GL.iNet AR150, AR300M16*, and *AR750 Creta*. The AREDN |trade| firmware running on these types of nodes has the WAN port preconfigured for connecting to the Internet. You can get the latest information about the specific port configured as the node's WAN port from the AREDN |trade| website here: `Ethernet Port Usage <http://downloads.arednmesh.org/snapshots/readme.md>`_

.. image:: _images/home-router-connection.png
   :alt:  Connect nodes to Internet through home router
   :align: center

When you connect the node's WAN port to one of the LAN ports on your home router, the node's WAN should receive an IP address on your home network from the router's `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ server. Alternatively you can reserve an IP address in your home network range and assign the static IP to the node's WAN through the **Basic Settings** page on your node. There are many sources of information about basic `home networking <https://en.wikipedia.org/wiki/Home_network>`_ which will not be duplicated here, but feel free to familiarize yourself with IP networking through reading and research.

Once you have connected your node to your home router, Internet access will be available to the node itself as well as to any of the devices connected to the node's LAN network. It is not recommended to allow Internet access through your node from other Mesh RF connected nodes, therefore be sure to leave *"Allow others to use my WAN"* unchecked. If you do not want any of your node's LAN connected devices to access the Internet either, you can check *"Prevent LAN devices from accessing WAN"*.
