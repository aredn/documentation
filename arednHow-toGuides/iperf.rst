=============================
Test Network Links with iperf
=============================

`iperf <https://en.wikipedia.org/wiki/Iperf>`_ is a network bandwidth testing tool which is available as an AREDN |trade| package for use on mesh nodes. It is a client-server utility, so it must be available on each node that will participate in the network test scenario. The iperf client node generates traffic which is sent to the server node. TCP bandwidth is measured and an estimate of the network speeds between that client and server is displayed.

Understand the impact to your network before using iperf. During the test period iperf will generate a significant amount of traffic in order to determine the capacity of the link between the client and server nodes. Try to run your iperf testing during times when you know that there will be minimal impact to users and routine traffic on your network.

Installing iperf and IperfSpeed
-------------------------------

Two packages should be installed on each AREDN |trade| node in order to facilitate testing between nodes. The `iperf3 <http://downloads.arednmesh.org/releases/3/18/3.18.9.0/packages/mips_24kc/base/iperf3_3.5-1AREDN_mips_24kc.ipk>`_ package allows the nodes to function either as an iperf client or server during the test. The `iperfspeed <https://s3.amazonaws.com/aredn/iperfspeed_0.5_all.ipk>`_ package provides a web-based control interface for running network tests between the nodes.

Using IperfSpeed
----------------

After iperf and IperfSpeed are installed on your nodes, you can select the *IperfSpeed* service on one of the nodes to open its web interface in a new browser tab. From the dropdown lists, select a node as the iperf server and also one as the iperf client. Click the *Run Test* button to begin the network bandwidth test.

.. image:: _images/iperfspeed-display.png
   :alt: iperfSpeed Display
   :align: center

Once the test has completed you will see the collected data summarized by time interval, and at the bottom of the display is the overall average of the results from the perspective of the sender (client) and the receiver (server). IperfSpeed also tracks previous tests that have been run, and it allows you to rerun any of the previous tests by clicking the *Re-Test* button.

One of the many uses for IperfSpeed is to validate and optimize your node's *Distance* setting on the **Basic Setup** page. Try different *Distance* settings and note the network bandwidth using iperf, with the goal of choosing the *Distance* setting which yields the best network performance.


.. |trade|  unicode:: U+00AE .. Registered Trademark SIGN
   :ltrim:
