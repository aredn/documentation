========================
Selecting Radio Hardware
========================

The amateur radio community has recognized the benefits of using inexpensive commercial :abbr:`WISP (Wireless Internet Service Provider)` radios to create AREDN® networks. Each of these devices comes with the vendor's firmware preinstalled, but by following documented procedures this firmware can be replaced with an AREDN® firmware image.

Several open source software projects have been adapted and enhanced to create the AREDN® firmware, including `OpenWRT (Open Wireless Router) <https://en.wikipedia.org/wiki/OpenWRT>`_ and `OLSR (Optimized Link State Routing protocol) <https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol>`_.

The AREDN® team builds specific firmware images tailored to each type of radio, and the current list of supported devices is found on the AREDN® website. For a complete list of all supported hardware, including both *Stable Release* and *Nightly Build* firmware, refer to the `Supported Devices <http://downloads.arednmesh.org/snapshots/SUPPORTED_DEVICES.md>`_ list. If at all possible try to avoid using devices listed under the *Sunset* heading, since those older devices are being retired.

When selecting a device for your AREDN® hardware there are several things to consider in your decision.

- Radios should be purchased for the specific frequency band on which they will operate. Currently AREDN® supports devices which operate in several bands. Check the `frequency and channel chart <https://docs.arednmesh.org/en/latest/appendix/freq_charts.html>`_ on the AREDN® website for the latest information.

- Radios can be purchased separately from the antenna, so it is possible to have more than one antenna option for a radio in order to optimize AREDN® nodes for varying deployment conditions.

- Costs of devices range from $25 to several hundred dollars for a complete node/antenna system, so there are many options even for the budget-conscious operator.

- Some older or lower cost devices have a limited amount of onboard memory. Consider purchasing a device with more memory over one with less memory.

- Check the maximum power output of the device, since some devices have lower power capabilities.

One of the best sources of detailed hardware information is a manufacturer's datasheet, usually available for download from the manufacturer's website. Currently AREDN® supports dozens of device models from manufacturers including GL-iNet, Mikrotik, TP-LINK, and Ubiquiti Networks.

If you are just getting started with AREDN® you can easily begin with one of the low-cost devices that comes with an integrated antenna and a :abbr:`PoE (Power over Ethernet)` unit. If you are expanding your AREDN® network with more sophisticated equipment, you may choose a standalone radio attached to a high-gain antenna.

.. note:: See the **Network Design Guide** for more information about constructing robust mesh networks.
