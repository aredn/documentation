===================
Node Status Display
===================

Once you have completed the initial setup on your AREDN |trade| node, you can connect your computer to a :abbr:`LAN (Local Area Network)` port on the device or the :abbr:`PoE (Power over Ethernet)` and use a web browser to navigate to the **node status** page.
``http://localnode.local.mesh`` or ``http://<your-nodename>.local.mesh``

.. image:: _images/node-status-columns.png
   :alt: Node status display
   :align: center

This display has been designed to present all of the important information about your node in one place. Someone navigating to your node's status display will be able to see all of the key elements of interest without having to click to multiple pages. This display consists of a top bar, a left side bar, and three columns of information about your node.

Top Nav Bar
-----------

From left to right, after the AREDN |trade| logo, the node name is displayed along with a label indicating whether you are viewing the *status* or *admin* display.

|icon1| At the far right is the default icon indicating that you are viewing the page as a normal user. Clicking this icon will allow you to login as the node administrator.

|icon2| If this icon is displayed at the far right, then you are viewing the page as the node administrator.

Left Nav Bar
------------

Using the icons on the left side bar you can navigate to various displays.

  |icon3| navigates to this **node status** display.

  |icon4| navigates to the local mesh status page showing the nodes visible on the local mesh network, as well as any services are provided by those nodes.

  |icon5| navigates to the *Cloud Mesh* view through the Supernode network (if available).

  |icon6| navigates to the world map on the AREDN |trade| website.

Left Column
-----------

Several sections of node information are presented here (listed from top to bottom).

Node Description
  This is not a required field, but it is a good place to describe the features or function of this device. Many operators use this field to list their contact information or the tactical purpose for the node. There are no character restrictions in the field, but the maximum length allowed is 210 characters.

Node Time, Uptime, Load Average, and Free Memory
  The node time is displayed, as well as the ``uptime``, which is the time since the last reboot. If an Internet connection or a local :abbr:`NTP (Network Time Protocol)` server is available, your node's NTP client will sync its time with that time source. The ``load`` is the average system utilization for the last 1, 5, and 15 minutes. ``free flash`` and ``free ram`` shows how much storage space is remaining on your node. ``flash`` is the internal non-volatile storage where the operating system, configuration files, and software packages are kept. ``ram`` is the amount of :abbr:`RAM (Random Access Memory)` available for running processes on the node.

Firmware Information
  This displays the node's current firmware version. A badge on the right indicates the status of the firmware, with valid values including ``Up to date``, ``Update available``, and ``Custom``.

Network Information
  The Mesh IP address/netmask is displayed using `CIDR <https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing>`_ notation, followed by the :abbr:`LAN (Local Area Network)` IP address/netmask. If the :abbr:`WAN (Wide Area Network)` interface is enabled, the WAN IP address/netmask is displayed along with whether this address was obtained via `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ or assigned as a static IP address. The WAN gateway IP address is also displayed along with the IP(s) of the WAN `DNS servers <https://en.wikipedia.org/wiki/Domain_Name_System>`_.

Node Location Information
  At the bottom of the left column is the node location information. If the latitude, longitude, and grid square have been entered for this node, a thumbnail map will show its location and coordinates, with the latitude, longitude, and grid square printed below it.

Center Column
-------------

The center column has three main sections (listed from top to bottom).

Local Services
  This section displays the service links for any mesh services on your node or its locally-connected devices. These service links are displayed side by side in two columns. Clicking any of the links will navigate to the selected service.

Local Devices
  This section displays any devices that are directly connected to your node. This includes devices that are connected to your node's :abbr:`LAN (Local Area Network)` via Ethernet cable (such as :abbr:`VoIP (Voice over IP)` phones, IP cameras, or service computers). If a device is reachable from your node, you can click on the device name link to navigate to that device.

  .. note::
    ? IS THIS IMPLEMENTED ? --- If you have any hosts for which you selected *Do Not Propagate* in the **DHCP Reservations List**, those hosts will be displayed in a light gray color only on your node's *LAN Hostname* column. If you created any **DNS Aliases** for your hosts, those aliases will be displayed in a light orange color only on your node's *LAN Hostname* column. All other hosts will be displayed in the default color for the theme that you are using.

  If you hover the cursor over the device name, a popup will appear showing the relative link quality of the connection to that device. To the right of the device name there will be connectivity statistics, including :abbr:`lq (link quality)`, :abbr:`nlq (neighbor link quality)`, :abbr:`snr (signal to noise ratio)`, :abbr:`n snr (neighbor signal to noise ratio)`, :abbr:`errors (retransmission errors)`, :abbr:`mbps (kilobit/megabit per second throughput)`, and :abbr:`miles (distance from the device)`.

Neighbor Devices
  This section displays any nodes that are direct neighbors of your node, whether via :abbr:`RF (radio frequency)` (as indicated by the small radio signal icon to the right of the device name), :abbr:`DtD (Device to Device)` nodes connected via Ethernet cable (as indicated by the small double arrow icon to the right of the device name), a cross-link, or a tunnel over an Internet connection. If a device is reachable from your node, you can click on the device name to navigate to that device. If you hover the cursor over the device name, a popup will appear showing the relative link quality of the connection to that device. To the right of the device name there will be connectivity statistics, including :abbr:`lq (link quality)`, :abbr:`nlq (neighbor link quality)`, :abbr:`snr (signal to noise ratio)`, :abbr:`n snr (neighbor signal to noise ratio)`, :abbr:`errors (retransmission errors)`, :abbr:`mbps (kilobit/megabit per second throughput)`, and :abbr:`miles (distance from the device)`.

Link Quality Statistics
  There are several link quality statistics displayed for each connected node.

  - ``lq`` or Link Quality is your node's view of the percent of `OLSR (Optimized Link State Routing protocol) <https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol>`_ packets received from the neighbor node. These packets exchange mesh routing and advertised services information, and they include a sequence number that is used to identify missing packets. For example, if 7 of 10 packets sent by the neighbor were received, then the probability for a successful packet transmission from this neighbor is 7/10 = 0.7 = 70%. ``nlq`` or Neighbor Link Quality is the neighbor node's view of the percent of :abbr:`OLSR (Optimized Link State Routing protocol)` packets received from your node.

  - ``snr`` or Signal-to-Noise Ratio is expressed in decibels (dB). It represents the level of signal which is detectable over the background noise floor, so a higher number is better. *SNR* is shown for both sides of any radio links (local ``snr`` and neighbor ``n snr``).

  - ``errors`` represents the number of retransmission errors detected on the link.

  - ``mbps`` is an estimate of the data rate achieved across any radio (RF) link. This column may show zero if the data being transmitted between these nodes is not sufficient for the metric to be calculated.

Right Column
------------

The right column displays additional details about your node (listed from top to bottom).

Radio Information
  Your radio manufacturer and model are displayed at the top of the column. Next is the channel number and frequency range set on your radio, followed by the channel width (in :abbr:`MHz (Megahertz)`). Below that is the transmit power (in :abbr:`dBm (decibels in millivolts)`), the maximum distance (in miles), and the minimum :abbr:`snr (signal to noise ratio)` (in :abbr:`dB (decibels)`) set for communication with other :abbr:`RF (radio frequency)` nodes.

Antenna Information
  Your node's antenna information is listed next, including the type of antenna, including the azimuth, height above ground level, and tilt angle / elevation (if directional).

Mesh Information
  Next there are summary statistics showing how many nodes are currently visible on the network, as well as the total number of devices that exist on the mesh.

DHCP Information
  By default each node runs a `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ server which is capable of automatically providing IP addresses for any LAN-connected devices. This section shows whether the :abbr:`DHCP (Dynamic Host Configuration Protocol)` server is enabled, and if so it displays the IP address/netmask of your node functioning as the gateway for its LAN-connected devices. It also shows the IP address range served by your node, any active leases, and any IP addresses that have been reserved for specific devices on its :abbr:`LAN (Local Area Network)`.

Tunnel Information
   This section displays statistics on any tunnel connections you may have on your node. The *Wireguard* section shows information for Wireguard tunnels, while the *Legacy* section shows information for the older vtun tunnels. Counts are displayed for active / allocated tunnel client connections as well as for active / allocated tunnel server connections on your node.



-------------------

.. |icon1| image:: ../_icons/login.png
  :alt: Normal user view

.. |icon2| image:: ../_icons/login-auth.png
  :alt: Admin user view

.. |icon3| image:: ../_icons/status.png
  :alt: Node status view

.. |icon4| image:: ../_icons/mesh.png
  :alt: Local mesh view

.. |icon5| image:: ../_icons/cloudmesh.png
  :alt: Cloud mesh view

.. |icon6| image:: ../_icons/map.png
  :alt: World map view
