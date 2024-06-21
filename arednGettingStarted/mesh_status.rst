===================
Mesh Status Display
===================

|icon1| You navigate to the **mesh status** page by clicking the mesh icon in the left nav bar.

.. image:: _images/mesh-status-columns.png
   :alt: Mesh Status display
   :align: center

|

At the top of this page there is a search box which allows you to filter the mesh network display to include only those devices which match the keywords you enter. As you type each character from your keyboard into the search field, the display will change to show only the entries that match your character string. The filter is case insensitive, so it will find both uppercase and lowercase entries for the characters you enter. To restore the original display, delete your search characters or refresh the page in the web browser. To the right of the search field there is a ``Help`` button which explains the use of the **mesh status** page.

The **mesh status** page is divided into several groups of devices, based on the link quality. The top groups are more likely to be reachable by your node than are the nodes in groups toward the bottom of the page.

Within each group the nodes are displayed side by side in two columns. The node in the upper left will have the best link quality, followed by the next best node to its right. Hovering the cursor over the left or right column will display a light gray background, making it easy to see which node you are focused on. You can navigate directly to that node by clicking on the node name.

Each node block will show the node name followed by a number that represents the :abbr:`ETX (Expected TX metric)`, which is an estimate of the number of :abbr:`OLSR (Optimized Link State Routing protocol)` packets that must be sent in order to receive a round trip acknowledgment, and it is often referred to as *link cost*. When sending data the :abbr:`OLSR (Optimized Link State Routing)` protocol selects the least cost route based on the lowest :abbr:`ETX (Expected TX metric)` in the direction of the final destination. Nodes are put into groups based on their :abbr:`ETX (Expected TX metric)`.

The display shows each node as well as any connected :abbr:`LAN (Local Area Network)` devices, as well as the advertised services available on the node and its hosts. You can click any available web links to navigate to the nodes or services listed.


.. |icon1| image:: ../_icons/mesh.png
  :alt: Local mesh view
