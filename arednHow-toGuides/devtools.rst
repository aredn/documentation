=====================
Tools for Integrators
=====================

This section of the AREDN® documentation contains information useful for people who want to retrieve information from one or more nodes for use in different applications. For example, an integrator may want to periodically poll a set of nodes to gather link quality or signal values to insert them into a network management or historian system for trending and analysis.

SYSINFO.JSON
============

The **sysinfo.json** `API (Application Programming Interface) <https://en.wikipedia.org/wiki/Application_programming_interface>`_ has been included in AREDN® firmware for several releases, and each release includes an *api_version* tag which can be used to track the feature set supported by that version of the API. As new features are added, the *api_version* number is incremented.

The basic API retrieves general node information in JSON format, and it can be invoked using the following URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json``

The following information is always returned in the JSON data stream:

- Node name
- API version
- Latitude, longitude, and grid square (if available)
- *Node Details* section containing the firmware manufacturer and version, the radio model and board ID, WAN sharing status, and the node description text (if any)
- *Sysinfo* section containing node uptime and load averages for the last one, five, and fifteen minutes
- *Interfaces* section containing the name, MAC address, and IP address (if any) assigned to each of the node's network interfaces
- *Mesh* section containing the SSID, channel, center frequency, channel width, and status of the mesh radio
- *Tunnels* section showing whether the tunnel package is installed and the number of active tunnels (if any)

The values returned by the API are represented in the following snippet of raw JSON. This is only a sample of the full data stream containing all of the values described above.

::

  {
  "api_version": "1.11",
  "lat": "33.101010",
  "lon": "-101.101010",
  "grid_square": "DM22xx",
  "node": "CALLSIGN-NODE-22",
  "sysinfo": {
    "uptime": "5 days, 6:22:30",
    "loads": [
      0.05003,
      0.05003,
      0
      ]
    },
  "node_details": {
    "description": "CALLSIGN-NODE-22 information here...",
    "mesh_gateway": "0",
    "model": "MikroTik RouterBOARD 952Ui-5ac2nD ",
    "board_id": "0x0000",
    "firmware_mfg": "AREDN",
    "firmware_version": "1101-ad0caaf"
    }
  }

In addition to the basic information described above, which is always returned with every invocation, the **sysinfo.json** API can also include other details based on the flags appended to the URL as explained below. In some cases it may be useful to include more than one of the following flags in the URL, and these flags can be combined using the ``&`` operator. For example, ``sysinfo.json?hosts=1&services=1`` will include both the *hosts* and *services* information in addition to the basic details which are always returned.

Add Hosts Information
---------------------

To retrieve mesh hosts information, invoke the API using the following flag on the URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json?hosts=1``

A *hosts* section will be included in the JSON data stream containing an entry for each node and mesh-connected device. The *name* and *IP* address of each device will be shown. The values returned by the *hosts* flag are represented in the following snippet of raw JSON.

::

  ...
  "hosts": [
    {
      "name": "CALLSIGN-NODE-22",
      "ip": "10.22.22.22"
    },
    {
      "name": "CALLSIGN-VOIP-PHONE",
      "ip": "10.22.22.24"
    },
    {
      "name": "MYCALL-NODE-81",
      "ip": "10.81.81.81"
    },
    {
      "name": "MYCALL-RPI",
      "ip": "10.81.81.83"
    }
  ],
  ...

Add Services Information
------------------------

To retrieve mesh services information, invoke the API using the following flag on the URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json?services=1``

A *services* section will be included in the JSON data stream containing an entry for each service available on the mesh. Each entry will include the service *name*, *protocol*, and *link* URL. The values returned by the *services* flag are represented in the following snippet of raw JSON.

::

  ...
  "services": [
    {
      "name": "IperfSpeed",
      "protocol": "tcp",
      "link": "http:\/\/MYCALL-NODE-81\/iperfspeed"
    },
    {
      "name": "EtherPad",
      "protocol": "tcp",
      "link": "http:\/\/MYCALL-RPI:9001\/"
    },
    {
      "name": "MeshChat",
      "protocol": "tcp",
      "link": "http:\/\/MYCALL-RPI\/meshchat"
    }
  ],
  ...

Add Local Services Information
------------------------------

To retrieve information about the services provided only through a single node, invoke the API using the following flag on the URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json?services_local=1``

A *services_local* section will be included in the JSON data stream containing an entry for each service available through the node being queried. Each entry will include the service *name*, *protocol*, and *link* URL as described above.

Add Link Information
--------------------

To retrieve mesh link information, invoke the API using the following flag on the URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json?link_info=1``

A *link_info* section will be included in the JSON data stream containing an entry for each node that is reachable via RF, :abbr:`DTD (Device To Device)`, or :abbr:`TUN (Tunnel)` from the node being queried. Each entry will be identified by the IP address of the reachable node, and within each IP address section you will see the *hostname* (node name), *linkType* (RF, DTD, or TUN), *linkQuality*, *neighborLinkQuality*, *signal*, *noise*, *olsrInterface* name, *tx_rate*, and *rx_rate*. The values returned by the *link_info* flag are represented in the following snippet of raw JSON.

::

  ...
  "link_info": {
    "10.22.22.22": {
      "hostname": "CALLSIGN-NODE-22",
      "linkType": "RF",
      "linkQuality": 0.9543000000,
      "neighborLinkQuality": 0.9748576110,
      "signal": -76,
      "noise": -95,
      "olsrInterface": "wlan0",
      "tx_rate": 6,
      "rx_rate": 4
    },
    "10.81.106.77": {
      "hostname": "MYCALL-NODE-81",
      "linkType": "DTD",
      "linkQuality": 1,
      "neighborLinkQuality": 1,
      "olsrInterface": "eth0.2"
    }
  },
  ...

Add LQM Information
-------------------

To retrieve Link Quality Monitor information, invoke the API using the following flag on the URL:
``http://<nodename>.local.mesh/cgi-bin/sysinfo.json?lqm=1``

An *lqm* section will be included in the JSON data stream showing the current LQM configuration settings as well as an entry for each node that is reachable via RF, :abbr:`DTD (Device To Device)`, or :abbr:`TUN (Tunnel)` from the node being queried. Each entry will be identified by the MAC address of the reachable node, and a variety of parameters will be displayed showing the tracked status of each link. The values returned by the *lqm* flag are represented in the following snippet of raw JSON.

::

  ...
  "lqm": {
    "enabled": true,
    "config": [],
    "info": {
      "coverage": 179,
      "trackers": {
        "02:7f:bd:83:e1:99": {
          "lon": -111.50478,
          "rev_ping_success_time": 0.07908412751042744,
          "babel_metric": 97,
          "ip": "10.204.12.202",
          "firstseen": 154,
          "ping_success_time": 0.021141793170887754,
          "localarea": true,
          "hostname": "ab7pa-hub",
          "rev_lastseen": 6194,
          "routable": true,
          "quality": 100,
          "user_blocks": false,
          "type": "DtD",
          "ping_quality": 100,
          "device": "br-dtdlink",
          "distance": 0,
          "lastseen": 6919,
          "babel_route_count": 2,
          "node_route_count": 149,
          "rev_ping_quality": 100,
          "refresh": 7095,
          "model": "MikroTik hAP ac2",
          "lat": 33.383020000000002,
          "rev_quality": 100,
          "mac": "02:7f:bd:83:e1:99",
          "firmware_version": "20250301-0bef22a0"
        }
      },
      "now": 6919,
      "total_node_route_count": 149,
      "distance": 80550,
      "hidden_nodes": []
    }
  }
  ...
