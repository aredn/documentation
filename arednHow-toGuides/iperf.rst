==============================
Test Network Links with iperf3
==============================

`iperf3 <https://en.wikipedia.org/wiki/Iperf>`_ is a network throughput testing tool which is now included in the AREDN |trade| firmware by default. It is a client-server utility, so it must be running on each node that will participate in the network test scenario. The iperf3 client node generates traffic which is sent to the server node. Network throughput is measured and an estimate of the network speeds between that client and server is displayed.

Understand the impact to your network before using iperf3. During the test period iperf3 will generate a significant amount of traffic in order to determine the capacity of the link between the client and server nodes. Try to run your iperf3 testing during times when you know that there will be minimal impact to the routine traffic on your network.

Installing IperfSpeed
---------------------

The **IperfSpeed** package provides a web-based control interface for running network tests between nodes, and it was written by Trevor Paskett K7FPV using the Perl programming language. With the project to retire Perl on AREDN |trade| nodes, there is now an alternative *IperfSpeed* package which uses the Lua programming language. The original Perl and new Lua packages are available at the following links:

- `Original Perl version of IperfSpeed <https://aredn.s3.amazonaws.com/iperfspeed_0.5.1_all.ipk>`_

- `New Lua version of IperfSpeed <https://github.com/kn6plv/iperfspeed/raw/master/iperfspeed_0.6-lua_all.ipk>`_

Using IperfSpeed
----------------

Select the *IperfSpeed* service on one of the nodes to open its web interface in a new browser tab. From the dropdown lists, select a node as the iperf3 server and also one as the iperf3 client. Click the *Run Test* button to begin the network throughput test.

.. image:: _images/iperfspeed-display.png
   :alt: iperfSpeed Display
   :align: center

|

Once the test has completed you will see the collected data summarized by time interval, and at the bottom of the display is the overall average of the results from the perspective of the sender (client) and the receiver (server). IperfSpeed also tracks previous tests that have been run, and it allows you to rerun any of the previous tests by clicking the *Re-Test* button.

One of the many uses for IperfSpeed is to validate and optimize your node's *Distance* setting on the **Basic Setup** page. Try different *Distance* settings and note the network throughput using iperf3, with the goal of choosing a *Distance* setting which yields the best network performance.
