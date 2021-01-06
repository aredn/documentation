===================
Networking Overview
===================

This **Network Design Guide** will discuss some of the useful principles for creating robust data networks as a service both to the amateur radio hobby and the community at large. An AREDN |trade| network is able to serve as the transport mechanism for the applications people rely upon to communicate with each other in the normal course of their business and social interactions, including email, chat, phone service, document sharing, video conferencing, and many other useful programs. Depending on the characteristics of the implementation, this digital data network can operate at near-Internet speeds with many miles between network nodes.

There are a variety of ways to interconnect AREDN |trade| nodes, but the most important question that should be answered is *"What is the purpose for this particular network?"* The specific requirements of your situation will drive the design of your data network. For example, consider the following issues.

Temporary or Permanent
  Is your network being deployed as a short-term communication mechanism, possibly to meet the needs of a day-long event or a training exercise? If so, then several amateur radio operators with portable nodes can quickly establish an *ad hoc* network with a specific set of services to meet the communication needs for that situation. Those nodes and computers can probably operate from portable batteries, without any external power dependencies for such a limited-time deployment.

  Is your network intended as a long-term or permanent infrastructure to serve the on-going communication needs of a local area or region? If so, then a more sophisticated network topology must be designed and constructed to meet those long-term requirements. More robust or ruggedized radio equipment may be necessary, and more reliable AC power or off-grid renewable energy resources will be required to ensure consistent operations.

Geography and Terrain
  Where is data communication needed? Are there specific locations where network nodes are required? What level of :abbr:`RF (Radio Frequency)` coverage will be needed in order to reach those locations? The places that the network must reach will determine the number and position of AREDN |trade| nodes.

  What are the geographical characteristics of the area across which your data network will operate? Different types of terrain may require specific types of network connections in order to adequately cover the region over which data communications are needed. More demanding terrain may require a larger number of intermediate nodes or possibly larger higher-gain antenna systems and mounting structures.

Expansion and Growth
  Will your network need to expand or adapt to changing conditions over time? Mesh networks are ideally suited for *ad hoc* growth and least cost routing based on the availability of nodes. As more devices are added to the network, however, the topology becomes more complicated and data traffic may be routed through multiple "hops" in order to reach its intended destination. This could result in increased latency on the network, with some network segments becoming almost unusable if application response time thresholds cannot met.

Applications and Throughput
  What network programs, applications, or services should be provided in order to fulfill the purpose for this network? Each application will generate a certain amount of data traffic, and some programs or services are more data-intensive than others. The network needs to be designed to adequately pass the traffic for the required applications.

  How many simultaneous users will be generating network traffic at different times? As the number of users increases, the amount of data traversing the network will also increase. In addition, with an increasing number of nodes on the network there will be a corresponding increase in the amount of `OLSR (Optimized Link State Routing protocol) <https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol>`_ traffic that is necessary to maintain the mesh network. An AREDN |trade| network should be designed to handle the expected workload.

With these issues in mind, it is always best to keep your network as simple as possible and to include only those services which are required. Be sure to design your network so that it accomplishes its mission and suits its intended purpose.
