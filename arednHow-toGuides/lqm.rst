==========================
Link Quality Manager (LQM)
==========================

*Contributor: Tim Wilkerson KN6PLV*

AREDN® mesh networks often lack the bandwidth you might expect. Here we look at what may be happening, a proposal to fix it, and results from these fixes.

Introduction
------------

This document describes *Link Quality Manager* which is enabled on nodes to better manage RF links. Typically 3x bandwidth improvements have been observed, but much higher improvements are possible.

Expected link speed vs. actual link speeds
------------------------------------------

We’ve all pointed an AREDN® node at another node, found the sweet spot for the best SNR, and then been underwhelmed by how little bandwidth seems to be available. WiFi is famous for over-reporting how much bandwidth is available vs. what you actually get (think 1/6th in many cases), but somehow we all expect a 2 mile link with SNR > 20 to do more than 1 Mbps. Unfortunately actual performance data is difficult to come by, and experiments to see what might improve are difficult to coordinate. Several theories are described below.

Performance theories
--------------------

Hidden nodes
^^^^^^^^^^^^

The classic problem with CSMA networks like AREDN® is that of “hidden nodes”. CSMA works by nodes listening for transmitters before themselves transmitting. This can fail when nodes are spread out so only some nodes can hear others resulting in many transmitting simultaneously, corrupting data, requiring retransmissions, and wasting bandwidth.

While this could be a real issue for AREDN® networks, it only has an effect when there are a lot of collisions. For there to be a lot of collisions there has to be a lot of traffic ... but AREDN® networks are largely idle. Probably the biggest traffic generator is OLSRD, and on the SF Bay Area network (for example) OLSR accounts for only a few kilobytes/second. Statistically it is difficult to ascribe the bandwidth problems to hidden nodes.

Bandwidth decimation
^^^^^^^^^^^^^^^^^^^^

Bandwidth decimation occurs when too many radios are using the same channel at similar locations, and so rather than adding bandwidth each radio ends up with a share of the original.

As noted above, AREDN® doesn’t currently use much of its available bandwidth. There is some overhead in having multiple radios on the same channel, even if they are not very active, but it is not significant. Compare this to a home wifi setup: if many devices are constantly using a lot of bandwidth then it is definitely noticeable.

Checking the status of various omnidirectional antennas on the SF Bay Area network (for example), there are rarely more than five neighbors on each node and never more than ten. If everyone were transmitting constantly there would be a problem, but this does not occur often.

CSMA vs. TDMA
^^^^^^^^^^^^^

TDMA is more efficient than CSMA and avoids many of its problems. However, Linux currently has no implementation of the protocol; it is restricted to proprietary radios. This means that AREDN® as currently envisaged cannot support TDMA. While TDMA radios may have a place in an AREDN® network, they seem better suited for backbone operation.

That said, racing to embrace TDMA without understanding why the current CSMA network is failing is problematic. If hidden nodes aren’t the issue, and network utilization is too low for bandwidth decimation, how would TDMA fix this? What actually is the problem?

Alternate theory
----------------

Coverage Class
^^^^^^^^^^^^^^

The WiFi standard (IEEE Std 802.11TM-2007, Part 11) briefly discusses “Coverage Classes”. This defines the air time propagation for the wifi signal. For in-home networks this parameter is unimportant as devices are close together, and the actual time it takes for packets to transfer between devices is essentially zero. However, for long distance networks this parameter becomes more important. A wifi signal propagates at approximately one mile every five microseconds. This seems fast but it quickly becomes significant especially over 10 and 20 mile links. Coverage Class is designed to account for wifi propagation time. If the Coverage Class is too high, devices will wait longer than necessary to retransmit failed packets. If the class is too low, devices will retransmit packets unnecessarily. Having an appropriate Coverage Class for a long distance network link is very important for optimal performance.

Auto-distance
^^^^^^^^^^^^^

Legacy AREDN® firmware versions provided a “Distance to FARTHEST Neighbor” setting which, indirectly, allowed the Coverage Class to be set (the Linux kernel calculates the coverage class from the distance setting). An “auto” option was provided and enabled by default. “Auto” uses a “dynamic ack” algorithm in the kernel which automatically adjusts the Coverage Class. The adjustment is based on the timing of packets sent to and acknowledged from other devices. The class will always be large enough to handle the most distant device.

AREDN® is an open *ad hoc* network allowing any node to associate with any other node as long as it uses the same channel and bandwidth. This results in distant nodes with very low SNRs being associated with each other. Unfortunately the dynamic-ack algorithm does not know that these links are essentially unusable, but it still adjusts the Coverage Class to accommodate them. The result is a higher Coverage Class than is required for optimal network operation, resulting in longer delays in packet retransmission. This compounds the already increased retransmissions inherent in longer links and further reduces the throughput.

Link Quality Manager (LQM)
--------------------------

*Link Quality Manager* is enabled on any node running firmware 3.22.12.0 or newer. It runs in the background to evaluate links and automatically takes the following actions: 

1. Blocks radio links which are also DtD links
2. Blocks radio links which have too low an SNR
3. Blocks radio links which are too distant
4. Blocks radio links with too many retransmission errors
5. Sets the node’s Coverage Class based on the most distant non-blocked node that is a direct, routable neighbor.

What does this mean?
^^^^^^^^^^^^^^^^^^^^

1. Occasionally nodes are directly connected (DtD) to collocated nodes which are also using the same channel. Although the DtD link should be preferred by OLSRD, LQM ensures that any radio link between DtD nodes is always ignored.

2. LQM ignores links with SNR too low to be useful. The application uses adjustable settings to accomplish this: drop below the minimum SNR and the link is blocked until the SNR is above the activate level. The hysteresis avoids links bouncing in and out of a blocked state. This stops OLSR from using poor links.

3. LQM limits how far a node can be from a neighbor and still have a reliable link, even if there is a high SNR. The more distant a node, the lower the throughput of the link. In addition, the total throughput on a node is affected by the most distant node it communicates with. LQM automatically determines the distance between nodes using the latitude and longitude information available from each node’s sysinfo.json api.

4. Some links can have high SNR, not be far away, but still have terrible performance due to excessive retransmission errors. While some retransmissions are to be expected, if this rate becomes large then performance suffers. LQM blocks links with poor link quality.

5. LQM disables automatic distance detection and takes over the job of managing the Coverage Class. LQM evaluates the non-blocked links and determines whether there is at least one route which uses this link. It then selects the link with the largest distance and uses this to calculate the Coverage Class.

The *Link Quality Manager* refreshes its state every minute and adjusts the blocked nodes and Coverage Class calculations. The *node status* display shows statistics for each link. LQM settings can be adjusted on the **Radios & Antennas** display.

What LQM does not do
^^^^^^^^^^^^^^^^^^^^

LQM blocks nodes by blocking traffic from the appropriate MAC addresses. What it does not do is prevent nodes from associating with the radio. It would be ideal to either ban “poorly performing” nodes from associating with a radio, or alternatively telling the node not to associate with distant radios. However, the ad-hoc wifi mode used in AREDN® does not currently support this.

Test Results
------------

LQM has been deployed and tested on a number of links with various radio environments and properties, both in the San Francisco Bay Area as well as in Southern California. Early feedback from these experiments have helped to refine and improve LQM and the results presented below are from version ``0.4``.

In the tables below we list various links of different lengths which were tested with and without LQM. Where possible the signal-to-noise ratio at both ends of the link were noted. Bandwidths were measured using multiple runs of *iperf3* in both directions (the results separated by slashes). Additional notes highlight information relevant to the nodes and related tests.

SF Bay Area Network
^^^^^^^^^^^^^^^^^^^

=====================  =====  =============  ===============  =============
Link Distance (miles)  SNR    No LQM (Mbps)  With LQM (Mbps)  Notes
=====================  =====  =============  ===============  =============
2                      25/28  0.282/2.79     13.3/20.6        Channel 177, very congested in this area
2                      36/31  38.8/32/6      50.4/50.9        Channel 173, 20 MHz, no congestion
=====================  =====  =============  ===============  =============

Southern California Network
^^^^^^^^^^^^^^^^^^^^^^^^^^^

=====================  =====  =============  ===============  =============
Link Distance (miles)  SNR    No LQM (Mbps)  With LQM (Mbps)  Notes
=====================  =====  =============  ===============  =============
4                             6.4/6.3        11.3/11.0        Links running from single node to 3 other nodes with similar distances, some congestion
5                             11.4/11.1      16.0/15.8
5                             9.2/9.1        16.7/16.4
11                            2.5/2.2        9.6/9.4
20                            4.9/4.7        4.8/4.6          Congested site with a mix of short and very long links
34                            0.7/0.6        0.7/0.7
=====================  =====  =============  ===============  =============

These results yield the following conclusions:

- LQM never negatively affects bandwidth, but the positive effect can be very large.

- The only result where there was no measurable improvement was at a site having a mixture of many long and short distance links. As expected, the very long 34 mile link negatively impacted all other links on that radio.

- Improvements of 47x were observed in one case (which was verified multiple times) and it occurred in a crowded, noisy environment. More typical improvements were around 3x.

Conclusions
-----------

Experiments with *Link Quality Manager* have demonstrated that we can improve the throughput on links by a significant amount without making physical changes to the network. Improvements of 3x bandwidth are common and in many cases much more is observed.

LQM also blocks paths in the network which are marginal, either due to excessive distance, poor SNR, or high retransmissions. We expect that by blocking poorly performing links the entire network will be more stable and performant.

Nodes with a mix of long and short links showed less improvement because the radio is optimized for the longer link distance. This increases retransmissions delays on the shorter links, reducing the throughput and lowering overall node performance. It might be better to use two radios at those sites to offload the longer links.
