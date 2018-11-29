========================
Selecting Radio Hardware
========================

The amateur radio community has recognized the benefits of using inexpensive commercial :abbr:`WISP (Wireless Internet Service Provider)` radios to create AREDN |trade| networks. Each of these devices come with the vendor's firmware pre-installed, but by following a few simple steps this firmware can be replaced with an AREDN |trade| firmware image. Several open source software features have been adapted and enhanced to create the AREDN |trade| firmware, including :abbr:`OpenWRT (Open Wireless Router)` and :abbr:`OLSR (Optimized Link State Routing protocol)`. The AREDN |trade| team builds specific firmware images tailored to each type or version of radio, and the current list of supported devices is found on the AREDN |trade| website in the `Supported Platform Matrix <https://www.arednmesh.org/content/supported-platform-matrix/>`_.

When selecting a device for your AREDN |trade| hardware there are several things to consider in your decision.

* Radios should be purchased for the specific frequency band on which they will operate. Currently AREDN |trade| supports devices which operate in the 900 MHz, 2.4 GHz, 3.4 GHz, and 5.8 GHz bands.
* Many devices come with an integrated dual-polarity :abbr:`MIMO (Multiple Input-Multiple Output)` antenna which helps to mitigate multipath propagation issues.
* Radios can be purchased separately from the antenna, so it is possible to have more than one antenna option for a radio in order to optimize AREDN |trade| nodes for varying deployment conditions.
* Costs of devices range from $50 to several hundred dollars for a complete node, so there are many options even for the budget-conscious operator.
* Some older or lower cost devices have a limited amount of onboard memory, but firmware images continue grow in size and functionality. Consider purchasing a device with more memory over one with less memory.
* Check the maximum power output of the device, since some devices have lower power capabilities.

One of the best sources of detailed device information is a manufacturer's datasheet, usually available for download from the manufacturer's website. Currently AREDN |trade| supports over fifty device models from the following manufacturers: Mikrotik, TP-LINK, and Ubiquiti Networks.

If you are just getting started with AREDN |trade| you can easily begin with one of the low-cost devices that comes with an integrated antenna and a :abbr:`PoE (Power over Ethernet)` unit. If you are expanding your AREDN |trade| network with more sophisticated equipment, you may choose a standalone radio attached to any of several kinds of high-gain antennas.

.. note:: See the **AREDN Design Guide** for more information about constructing robust mesh networks.


.. |trade|  unicode:: U+02122 .. TRADE MARK SIGN
   :ltrim:
