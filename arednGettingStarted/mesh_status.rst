===================
Mesh Status Display
===================

The **Mesh Status** page lists mesh nodes and link quality information, along with any LAN hosts and advertised services available on the network. Below the node name bar there are several controls.

- The **Refresh** button refreshes the *Mesh Status* display with current information.

- The **Auto** button sets the display to automatically refresh the node information every 10 seconds. To end auto-refresh mode, click **Stop** or **Quit**. *Stop* returns to the static *Mesh Status* display. *Quit* takes you back to the *Node Status* display, but clicking *Mesh Status* again from there will return you to auto-refresh mode on the *Mesh Status* display.

- The **Cloud Mesh** button allows you to navigate to the *Mesh Status* display of the closest Supernode available to your device. Supernodes are a way to link multiple mesh island networks in a safe and efficient way. If your local node is part of a network with a Supernode, then you have the ability to view other nodes which are part of the Cloud Mesh network even if your local mesh is not otherwise linked to those networks. For further information see the *Supernode Architecture* description in the **Network Topologies** section of the **Network Design Guide**.

- The **Quit** button returns you to the *Node Status* display.

- The **Search** field allows you to filter the *Mesh Status* display by any keywords of your choice. The display will be limited to showing only nodes which match the keywords you enter. As you type each character from your keyboard into the search fields, the display will change to show only the entries that match your character or string. The filter is case insensitive, so it will find both upper and lower case entries for the characters you enter. If you press the **Refresh** button on the *Mesh Status* display, the search field will be cleared.

.. image:: _images/mesh-status.png
   :alt: Mesh Status
   :align: center

|

Node Name
^^^^^^^^^

This shows your node as well as any connected LAN hosts and the advertised services available on your node and hosts. You can click any available web links to navigate to the services on your node or LAN hosts. This will be true for any available services in the *Current Neighbors* or *Remote Nodes* sections, too. Each node will be highlighted as you hover your cursor over it. This gives a visual indicator for any column entries that are part of the row over which you are hovering.

If you have any hosts for which you selected *Do Not Propagate* in the **DHCP Reservations List**, those hosts will be displayed in a light gray color only on your node's *LAN Hostname* column. If you created any **DNS Aliases** for your hosts, those aliases will be displayed in a light orange color only on your node's *LAN Hostname* column. All other hosts will be displayed in the default color for the theme that you are using.

Current Neighbors
^^^^^^^^^^^^^^^^^

This shows a list of *Neighbor Nodes* that are linked with your node. These nodes may be connected via radio, Device-to-Device link (dtd), a cross-link (xlink) or a tunnel (tun) over an Internet connection. The display also shows any LAN hosts on your current neighbors as well as any advertised services available on those nodes and hosts.

Link Quality Statistics
  There are several link quality statistics displayed for each connected node.

  - ``LQ`` or Link Quality is your node's view of the percent of `OLSR (Optimized Link State Routing protocol) <https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol>`_ packets received from the neighbor node. These packets exchange mesh routing and advertised services information, and they include a sequence number that is used to identify missing packets. For example, if 7 of 10 packets sent by the neighbor were received, then the probability for a successful packet transmission from this neighbor is 7/10 = 0.7 = 70%. Be aware that the *Quality* metric is calculated differently, so there may not be a perfect alignment when comparing the two quality metrics.

  - ``NLQ`` or Neighbor Link Quality is the neighbor node's view of the percent of :abbr:`OLSR (Optimized Link State Routing protocol)` packets received from your node. This indicates the quality of the link from the neighbor's side.

  - ``SNR`` or Signal-to-Noise Ratio is expressed in decibels (dB). It represents the level of signal which is detectable over the background noise floor, so a higher number is better. *SNR* is shown for both sides of any radio links (local SNR / remote SNR).

  - ``Quality`` is the Link Quality calculated as the moving average of (total sent packets) divided by (total sent packets plus retransmissions), expressed as a percent. For example, if the node had to send every packet twice for it to be successfully received, the link quality would be 50%. An additional penalty is subtracted if the neighbor node is unpingable, which is explained in the *Advanced Configuration* section under "Ping Penalty". Be aware that the *LQ/NLQ* metrics are calculated differently, so there may not be a perfect alignment when comparing the two quality metrics.

  - ``TxMbps`` or Transmit Megabits per Second is an estimate of the data rate achieved across any radio (RF) link with a neighbor node. This column may show zero if the data being transmitted between these nodes is not sufficient for the metric to be calculated.

  - ``Distance`` is the calculated distance between your node and each remote node. This calculation is based on the GPS coordinates (Lat/Lon) that were entered on each node. If no GPS coordinates were entered, then the distance cannot be calculated and that metric will not be considered in the LQM improvement process.

  - ``Service Name`` is the column which displays any available services on the neighbor node or its LAN hosts. You can click on service links to navigate to the webpage for those services.

In addition to the neighbor node name, there are text abbreviations in parentheses that tells how the neighbor node is connected and the status of the link.

Link Type
  - ``rf``: Note that there is no link type identifier for radio links, so links without one of the identifiers below can be considered ``rf`` links.
  - ``dtd``: indicates a direct *Device to Device* connection (typically using an Ethernet cable) between the nodes.
  - ``tun``: indicates the path to the neighbor node is over an Internet tunnel. ``(tun*?)`` next to a mesh node in the *Remote Nodes* column indicates the node has tunnel links over the Internet to connect mesh islands together. ``?`` is a number indicating the number of tunnel connections on that node.
  - ``xlink``: indicates a connection between the nodes that traverses cross-linked devices.

Link Status
  - ``wan``: the node has been configured as a *Mesh Gateway*. Typically this is a gateway to the Internet, but it may also be to another isolated network.
  - ``pending``: LQM is collecting data and evaluating the link.
  - ``active``: LQM determined that the link is viable and can be used.
  - ``blocked``: LQM determined that the link is unusable and has blocked it from use.
  - ``blocked - distance``: LQM determined that the remote node is either too close or too distant, based on the Min and Max Distance settings described in the *Advanced Configuration* section.
  - ``blocked - signal``: LQM determined that the SNR on the link is too low to reliably pass data, based on the Min SNR setting described in the *Advanced Configuration* section.
  - ``blocked - retries``: LQM determined that the retransmission rate is too high to reliably pass data.
  - ``blocked - latency``: LQM determined that the link latency is too high to reliably pass data.
  - ``blocked - dtd``: LQM blocks the RF interface on any nodes to which a DtD link also exists.
  - ``blocked - dup``: LQM blocks a link in cases when your node has an RF link to other nodes which themselves connect to each other via DtD. This can occur when there are multiple radios at a site using the same channel. The best remote node is chosen as the RF link for your node but the other possible RF connections are blocked as duplicates.
  - ``blocked - user``: LQM will block any node which you enter in the *User Blocked Nodes* field described in the *Advanced Configuration* section.
  - ``hidden``: LQM will display nodes that are out of range of your node but which are able to access a common intermediary node.
  - ``exposed``: LQM will display nodes that can reach other nodes which are hidden from your node.
  - ``idle``: LQM has determined that the link is usable and would be ``active`` but the node routing table does not yet have a route for sending traffic across the link.
  - ``disconnected``: This RF Neighbor is no longer online.

  You can refresh the *Link Status* values by pressing the *Refresh* button or by selecting the *Auto* button to automatically refresh the display. Links whose quality has improved may be activated, while links whose quality has worsened may be blocked.

Previous Neighbors
  If there were any Current Neighbors which disconnected within the last 24 hours they will be listed below any nodes that are currently connected. It shows the node name or IP address, as well as how long it has been since a node was actively connected to your node.

Remote Nodes
^^^^^^^^^^^^

This section lists the other nodes on the network that are two or more hops away from your node. Advertised services on nodes and their LAN hosts are also listed. Remote Nodes are sorted by their ``ETX`` or *Expected Transmission* metric. :abbr:`ETX (Expected TX metric)` is an estimate of the number of :abbr:`OLSR (Optimized Link State Routing protocol)` packets that must be sent in order to receive a round trip acknowledgement, and it is often referred to as *link cost*. When sending data the :abbr:`OLSR (Optimized Link State Routing)` protocol selects the least cost route based on the lowest :abbr:`ETX (Expected TX metric)` in the direction of the final destination.
