====================================
Tips for Aiming Directional Antennas
====================================

*Contributor: Brett Popovich KG7GDB*

AREDN® nodes with directional antennas can be challenging to align, especially if they have very narrow beam widths. The goal is to achieve the closest alignment in order to pass RF signals efficiently.

Practice with Nearby Nodes
--------------------------

If you can drive to within 1/4 mile of an active node, you should be able to pass signals well. At close range the aiming may not be as critical and you could even place a NanoStation or SXTsq panel on your dashboard. Find a public park, open parking lot, or street parking where you have line of sight to a remote node that uses the same frequency as your portable node. Here are some steps you can follow to practice aiming your node.

- In your vehicle, power up your node and plug in your laptop. Disable the wifi interface so the laptop gets its IP address from the node. Open a web browser and use ``http://localnode.local.mesh`` to load your node's home page. You will need to have your admin password to authenticate to *admin* mode.

- On the **Radio** page enter the SSID, channel, and channel width that matches the remote node you are surveying. If you changed any of these settings, click ``Done`` and ``Commit`` your changes.

- Now you can click the *Tools* icon to select **WiFi Signal** from the menu. Choose your remote node by clicking in the field at the right and selecting the desired remote node from the dropdown list. The signal level will be updated on the graph, and you can also enable an audio tone to give you an audible indication of the signal level. Turn your radio slowly or even change the car position to find the position at which the signal level is best.

- Once you have the highest SNR at your test location, click ``Done`` to return to the **node status** display. You should see the remote node in the list of *Neighborhood Nodes* in the center column. There will also be values displayed for the link quality. Hover over the row for the remote node and click to show the **Neighborhood Device** display. This will provide a wealth of information about the quality of the link to the remote node being tested.

- If desired you can click the neighbor node name to show the remote node's view of your connection by following the same procedure as above.

Aligning Distant Nodes
----------------------

Distant fixed nodes can be aligned with the same tools you used in the previous section. Different antennas will have different beam widths depending on the model. Check the manufacturer specifications to determine the beam width of your antennas. This will give you a clue as to how precise your aim should be in order to send/receive signals effectively.

For example, Mikrotik LHG5 and Ubiquiti RocketDish5 antennas are very narrow, with beam widths between 5° and 7°. Mikrotik QRT panels and Ubiquiti Powerbeam antennas have beam widths between 10° and 12°. Mikrotik SXTsq5 panels and Ubiquiti AirGrid antennas have beam widths between 20° and 23°. Ubiquiti NanoStations and Mikrotik SXTsq2 panels have beam widths between 45° and 60°. Sector antennas have typical beam widths of 90° or 120°, while omnidirectional antennas cover 360° with various degrees of downtilt.

.. image:: _images/beamwidth-comparison.png
   :alt:  Antenna beam width comparison
   :align: center

|

While it is helpful to know the antenna pattern for the nodes at both ends, the key is knowing the exact coordinates of the two locations so you can determine their topographical relationship to each other (horizontal and vertical azimuth). There are several computer tools for modeling radio links that were mentioned in the **Network Design Guide** under the *Network Modeling* section. One of the most useful is `VE2DBE's Radio Mobile <http://www.ve2dbe.com/rmonline.html>`_ which provides all of the required details for aiming directional antennas between two locations, including both true and magnetic bearings for both sides of the link.

Studying various local maps may allow you to discover other sites where you could place intermediate nodes that might link two distant locations. Google Earth can help you identify visible landmarks before aiming. Obvious tall objects such as water towers or multi-story buildings can be added as markers. Nearby objects such as church steeples or park features can be useful as visual reference points during the aiming procedure: for example, "I need to aim over the skate park to the left of the church to hit the remote node." Google Earth also provides a ruler tool which shows the bearing between map locations, and you can look at the Profile View to see whether there are features which may block your signal. Another tool mentioned in the **Network Design Guide** under the *Network Modeling* section is `Radio Fresnel <http://www.radiofresnel.com>`_ which generates a Google Earth KMZ file that identifies ground features which may block the Fresnel Zone along your link path.

.. image:: _images/link-azimuth.png
   :alt:  Antenna Aiming Details
   :align: center

|

The chart above shows typical link details that are provided by `Radio Mobile <http://www.ve2dbe.com/rmonline.html>`_. It is very helpful to know these kinds of details and to have an accurate compass before you begin the antenna aiming process. If you use magnetic bearings you will need to know the declination for your location, and be sure your phone or compass is not influenced by nearby metal objects.

Some antennas are easier to aim than others. Large metal dishes are heavy and may require two people to aim, whereas lighter dishes like the Mikrotik LHG units are easy to manipulate. Often only a slight change in position can make a large difference in SNR and link quality. Be sure to avoid trees and be sure your link's first Fresnel Zone is clear of obstructions in order to achieve the best link quality. See the **Network Design Guide** on *Radio Spectrum Characteristics* for examples of ground clearance at different frequencies to ensure the Fresnel Zone is clear.
