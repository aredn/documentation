================
Networking Tools
================

There are several service programs that can assist in visualizing or mapping an AREDN |trade| network, as well as for viewing local RF conditions near your node. Some of these programs are discussed below.

Manage Extra Static Routes
--------------------------

There may be cases when you need to create extra static routes to control the flow of network traffic through your node. You can maintain your extra routes by entering them into the ``/etc/aredn_include/static_routes`` file. You must login to your node at the command line and use the ``vi`` editor to manage the routes in this file. A helpful example is provided in the file, and you can view the `OpenWRT Static Routes <https://openwrt.org/docs/guide-user/network/routing/routes_configuration>`_ page for additional information about managing static routes.

AREDN |trade| Prometheus Exporter
---------------------------------

`Prometheus <https://en.wikipedia.org/wiki/Prometheus_(software)>`_ is an open-source monitoring and alerting toolkit which collects and stores metrics as time series data. At given intervals it can collect metrics from AREDN |trade| nodes having the ``prometheus-exporter`` package installed. Prometheus evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are detected.

AREDN |trade| metrics in the ``prometheus-exporter`` package include the following:

- Node details (name, model, firmware, description, Lat/Lon, grid square, band, channel, width, frequency, SSID)
- Memory, storage, CPU, and networking metrics
- RF metrics (signal, noise, MSC rate, TX/RX packets/rates)
- LQM metrics
- OLSR link info

In order for Prometheus to pull metrics from a node it will use the following target URL: ``http://<NODE>.local.mesh/cgi-bin/metrics`` and metrics are returned by the node as standard *text/plain* content. Minimal node resources are required to support Prometheus data collection since the node only uses minimal resources whenever this URL is queried.

.. image:: _images/prometheus-exporter.png
   :alt: Prometheus Exporter metrics in text format
   :align: center

|

The AREDN |trade| ``prometheus-exporter`` simply makes these metrics available for Prometheus to pull. For additional information about Prometheus itself, visit `their website here <https://prometheus.io/>`_. The following image shows Prometheus metrics for an AREDN |trade| node being displayed by the `Grafana <https://en.wikipedia.org/wiki/Grafana>`_ visualization application.

.. image:: _images/grafana.png
   :alt: Prometheus Exporter metrics in Grafana
   :align: center

|

KN6PLV Network Waterfall Scanner
--------------------------------

`Tim KN6PLV <https://www.qrz.com/db/KN6PLV>`_ created this program to assist with discovering the RF conditions around your node. It is installed as a node package which is available here: `KN6PLV Waterfall <https://github.com/kn6plv/waterfall>`_. Once installed, a new ``Waterfall`` button will appear on your *Node Status* page if the hardware supports it (the Waterfall scanner is not currently available on AC devices). It will disconnect your node from the mesh while it continuously scans for nearby RF signals, so it does require authentication with the node's login credentials in order to run. The *Spectral View* shows the strength of nearby signals, while the *Waterfall* maintains a record over time of the RF environment. This package does *not* work on node hardware having ``802.11ac`` chipsets.

.. image:: _images/waterfall-kn6plv.png
   :alt: KN6PLV Waterfall Display
   :align: center

|
