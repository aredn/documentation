=======================
AREDN Services Overview
=======================

As mentioned in the AREDN |trade| overview, the purpose of an amateur radio emergency data network is to provide typical Internet or intranet programs to people who need to communicate across a wide area during an emergency or community event. An AREDN |trade| network provides the transport mechanism for the types of programs people typically use today to communicate with each other in the normal course of their business and social interactions. This may include keyboard-to-keyboard chat, email messages with images and attachments, file transfer, collaborative document sharing, :abbr:`VoIP (Voice over IP)` phone service, video conferencing, :abbr:`GPS (Global Positioning System)` tracking, surveillance camera streaming, computer aided dispatch, deployed resource management, weather station reporting, sensor monitoring and control, repeater linking, and many other services.

The purpose for this section of the AREDN |trade| documentation is to identify the types of services that might be useful for communication across a mesh network. Almost any program that can operate across a peer-to-peer TCP/IP network is a candidate for AREDN |trade| networking, but you should carefully select and test your services to ensure they will work within the following guidelines.

* An important consideration for selecting programs is to understand the impact each service will have on the performance and reliability of the network during the times when digital communication is required. As a best practice, choose programs which require the least amount of computing and network resources in order to operate successfully.

* It is equally important to choose data services that meet the criteria defined in FCC Part 97 regulations for amateur radio services. Try to avoid programs that use encryption or proprietary compression algorithms, which may be interpreted as "encoding messages for the purpose of obscuring their meaning."

* As a general rule services should be run on separate LAN-connected computers rather than on the AREDN |trade| node itself. Radio nodes have very limited resources which should be conserved for node operation rather than running extra programs. Try to select external computers that have low power requirements, since many AREDN |trade| deployments are off-grid and without any external network access. Many operators use `Raspberry Pi <https://en.wikipedia.org/wiki/Raspberry_Pi>`_ computers which are small, easy to transport, and require minimal DC power for operation.

When choosing programs to use as AREDN |trade| services you will probably find that there is more than one way to accomplish your goals. It is crucial to clearly understand the types of communication that are required on your network, and then you will be able to select the best program for the job. Always try to use a program that will cause the least performance impact to your network as it is working to fulfill your communication needs.

Most TCP/IP programs are designed to use the `Client-Server <https://en.wikipedia.org/wiki/Client%E2%80%93server_model>`_ model, where one or more client programs communicate through a central server or servers distributed hierarchically. These types of programs will operate on a mesh network as long as the server is reachable on a readily accessible network segment with adequate bandwidth.

There are also programs which have been designed to take advantage of multiple paths between nodes and multiple peer servers coexisting on a mesh network. There are fewer of these mesh-friendly programs, but they will be identified as they appear in the following sections.

The remaining parts of this section focus on examples of services that could be offered on your AREDN |trade| network. Programs are grouped by type, and where possible the network impact of each program will be described in order for you to understand the resources that may be required to use the program as a service on the mesh.


.. |trade|  unicode:: U+02122 .. TRADE MARK SIGN
   :ltrim:
