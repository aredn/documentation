===============================
AREDN |trade| Services Overview
===============================

As mentioned in the AREDN |trade| overview, the purpose of an amateur radio emergency data network is to provide typical Internet or intranet programs to people who need to communicate across a wide area during an emergency or community event. An AREDN |trade| network provides the transport mechanism for the types of programs people typically use today to communicate with each other in the normal course of their business and social interactions. This may include keyboard-to-keyboard chat, email messages with images and attachments, file transfer, collaborative document sharing, :abbr:`VoIP (Voice over IP)` phone service, video conferencing, :abbr:`GPS (Global Positioning System)` tracking, surveillance camera streaming, computer aided dispatch, deployed resource management, weather station reporting, sensor monitoring and control, repeater linking, and many other services.

The purpose for this section of the AREDN |trade| documentation is to identify the types of services that might be useful for communication across a mesh network. Almost any program that can operate across a peer-to-peer TCP/IP network is a candidate for AREDN |trade| networking, but you should carefully select and test your services to ensure they will work within the following guidelines.

* An important consideration for selecting programs is to understand the impact each service will have on the performance and reliability of the network during the times when digital communication is required. As a best practice, choose programs which require the least amount of computing and network resources in order to operate successfully.

.. note:: The consideration above is especially important if you are deploying a service which regularly queries other nodes across the network. For example, if you deploy a network management system which polls metrics from remote mesh nodes, you need to carefully consider how many metrics you poll and how often you request them. Realize that polling dozens of metrics from each node every few seconds is likely to degrade mesh performance. Be sure to let node owners know what you are planning to do and get their permission/agreement for your polling schedule.

* It is equally important to choose data services that meet the criteria defined in FCC Part 97 regulations for amateur radio services. Try to avoid programs that use encryption or proprietary compression algorithms, which may be interpreted as "encoding messages for the purpose of obscuring their meaning."

* As a general rule services should be run on separate LAN-connected computers rather than on the AREDN |trade| node itself. Radio nodes have very limited resources which should be conserved for node operation rather than running extra programs. Try to select external computers that have low power requirements, since many AREDN |trade| deployments are off-grid and without any external network access. Many operators use `Raspberry Pi <https://en.wikipedia.org/wiki/Raspberry_Pi>`_ computers which are small, easy to transport, and require minimal DC power for operation.

When choosing programs to use as AREDN |trade| services you will probably find that there is more than one way to accomplish your goals. It is crucial to clearly understand the types of communication that are required on your network, and then you will be able to select the best program for the job. Always try to use a program that will cause the least performance impact to your network as it is working to fulfill your communication needs.

Most TCP/IP programs are designed to use the `Client-Server <https://en.wikipedia.org/wiki/Client%E2%80%93server_model>`_ model, where one or more client programs communicate through a central server or servers distributed hierarchically. These types of programs will operate on a mesh network as long as the server is reachable on a readily accessible network segment with adequate bandwidth.

**Keeping Multiple Servers in Sync**

Since the application *server* must be reachable on the network in order for *clients* to function, and since a solitary server can be a single point of failure, it may be useful to explore ways for redundant servers to be kept in sync across the network. If one server becomes unreachable, a backup or failover server could be used to keep the service running.

For mission-critical services on high speed data networks, *Disaster Recovery* designs are often implemented to ensure that services continue operating in the event of a failure. There are several methods for accomplishing this, which usually involve duplicating server hardware and software with some type of data replication between these systems. At a high level, two basic designs could be implemented as described below.

*Manual Failover Design*
  In this design there is a primary server that remains active, with a duplicate backup server located on another network segment. The standby server is brought online only if the primary server becomes unreachable. Application data on the primary server could be copied periodically to the standby server using an intelligent utility such as `rsync <https://en.wikipedia.org/wiki/Rsync>`_ running as a scheduled task which copies only what has changed since the last check. This design provides a fallback that can be used in case of emergency, but it requires some degree of manual intervention to bring up the standby service on the network when the primary becomes unreachable.

*Automated Failover Design*
  `High Availability <https://en.wikipedia.org/wiki/High-availability_cluster>`_ technology allows two or more sets of computing resources to send `heartbeat <https://en.wikipedia.org/wiki/Heartbeat_(computing)>`_ signals for detecting whether their services are available across the network. Several types of open source and commercial clustering packages are available, which provide varying degrees of complexity and recovery capabilities. Suffice it to say that many options are available for ensuring the availability of mission-critical services on your network. Feel free to research, investigate, and test several of these options if you have a pressing need for highly available mesh services.

.. image:: _images/server-sync.png
   :alt: Server Sync Diagram
   :align: center

As a general rule for mesh networks, simpler is better. The more complicated and automated you make your service design, the more network and computing resources will be required to operate the system. It is always best to conserve mesh networking resources wherever possible.

----------

There are also programs which have been designed to take advantage of multiple paths between nodes and multiple peer servers coexisting on a mesh network. There are fewer of these mesh-friendly programs, but they will be identified as they appear in the following sections.

The remaining parts of this section focus on examples of services that could be offered on your AREDN |trade| network. Programs are grouped by type, and where possible the network impact of each program will be described in order for you to understand the resources that may be required to use the program as a service on the mesh.


.. |trade|  unicode:: U+00AE .. Registered Trademark SIGN
   :ltrim:
