===============================
Creating a Local Package Server
===============================

There may be cases where your mesh nodes have no way to access the AREDN |trade| servers for installing new packages. One way to resolve this is to create your own package server on the local mesh and then point your nodes to this local service. The following sections describe the high-level tasks required to implement such a package service. In order to accomplish this, you may need to consult with someone who has System Administration skills for the specific platform you will be using to host your local package repository.

Configure your Package Server
=============================

Your package server must be connected to the mesh as a host on your local node's LAN network, using a node that also has Internet access via its WAN interface. The reason this node is connected to the Internet is to allow the web server to download updated files from the AREDN |trade| Internet server, but the node's Internet connection is not advertised or allowed for use by other nodes or devices on the mesh network. You should add this host to the node's *DHCP Reservation List*. You do not need to add the package host to the *Advertised Services List* of the node to which it is connected. The package server should be given a hostname that is unique on your mesh, typically prefixed with the callsign of the server owner. You can use any operating system platform you desire *(Windows, Linux, Mac),* as long as it has the ability to function as a web server. The following are the two main tasks required of the local package server:

* Obtain the set of AREDN |trade| software files from ``downloads.arednmesh.org``
* Make those files available via your computer's web server so nodes can query the package URLs

There are several ways to accomplish these tasks, and the best approach may vary depending on the platform you implement for your package server. Downloading the AREDN |trade| software files can be done manually as needed, or the process could be automated and executed on a regular schedule. Tools that could be used for this task include `HTTrack <https://en.wikipedia.org/wiki/HTTrack>`_ and `Wget <https://en.wikipedia.org/wiki/Wget>`_, both of which support recursive copying. You should try to make your local repository mirror the AREDN |trade| downloads directory tree as closely as possible, so it contains any of the package files you want to have available to your local mesh nodes.

Once you have downloaded the AREDN |trade| files, you need to make them available to network nodes via your web server. The steps for accomplishing this task will vary based on the specific web server software you are using. For example, Sys Admins using the `Apache Web Server <https://en.wikipedia.org/wiki/Apache_HTTP_Server>`_ might put the software files under their web server's *DocumentRoot*, or they might create an ``Alias`` to allow web access to parts of the filesystem that are not under the Apache *DocumentRoot* (as described `here <https://http
d.apache.org/docs/2.4/urlmapping.html>`_). Once the software has been made available via the web server, you should be able to enter that URL to navigate the entire package tree as shown below.

.. image:: _images/view-package-repo.png
   :alt:  View the local package repository
   :align: center

These tasks are all that should be required on your local package host. Once the package tree is available via its web server, you can begin pointing the nodes to your local software repository.

Point Nodes to the New Server
=============================

To point a node to the local software repository, navigate to **Setup > Advanced Configuration**. The table on this webpage has a row for each type of software that can be installed on AREDN |trade| nodes. It might be a good idea to take a screenshot of these settings so you can refer to them later. A typical default URL for *firmwarepath* is shown below:

::

  http://downloads.arednmesh.org/firmware

Simply replace this URL with the one that you configured on your local package host, then click the *Save Setting* button on that row. For example, the new entry for *firmwarepath* might look like the one below:

::

  http://ab7pa-box2.local.mesh/arednSoftware/firmware

It is good practice to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ so the node will be able to resolve the domain portion of the URL to the mesh host's IP address. The URL you enter should match exactly with the alias or path you created and tested on your web server as described in the previous section.

.. image:: _images/set-package-host.png
   :alt:  Advanced Configuration - set package URL
   :align: center

After you have entered the new URL, click the **Save Setting** button to activate the new entry. To restore the default entry, click the **Set to Default** button.

Once the node has been pointed to the local package repository, you can navigate to **Setup > Administration**. In the *Package Management* section, you can click the **Refresh** button to get the list of available packages from the local package repository. Remember that retrieving this package list will use memory resources on your node.

.. image:: _images/refresh-package-list.png
   :alt:  Administration - refresh package list
   :align: center

The following example shows the type of information returned when you click the **Refresh** button:

::

  Package Management

  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/base/Packages.gz
  Updated list of available packages in /var/opkg-lists/aredn_base
  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/base/Packages.sig
  Signature check passed.
  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/arednpackages/Packages.gz
  Updated list of available packages in /var/opkg-lists/aredn_arednpackages
  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/arednpackages/Packages.sig
  Signature check passed.
  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/luci/Packages.gz
  Updated list of available packages in /var/opkg-lists/aredn_luci
  Downloading http://ab7pa-box2.local.mesh/arednSoftware/snapshots/packages/mips_24kc/luci/Packages.sig
  Signature check passed.
  ...

Click the **Select Package** dropdown list to see the packages that are available for download to your node. Select a package and click the **Download** button. Status information will appear showing the actions that were taken to install the package from the local package host. A message may appear that a reboot is required to refresh and restart all services, but this is a normal status message and does not indicate an error condition.
