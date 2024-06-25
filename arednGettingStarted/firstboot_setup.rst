====================
Firstboot Node Setup
====================

After you have installed the AREDN |trade| firmware and rebooted the device, the node will have a default IP address of 192.168.1.1. Make sure your computer has an IP address on the 192.168.1.x network. After connecting your computer to a LAN port on the node or the :abbr:`PoE (Power over Ethernet)` unit, you should be able to ping the node at 192.168.1.1. Navigate to your node's web interface at ``http://192.168.1.1`` or ``http://localnode.local.mesh``. Some computers may have DNS search paths configured that require you to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ to resolve *localnode* to the mesh node's IP address. Each node will serve its web interface on ports 80 and 8080.

The firstboot status page will be displayed, instructing you to configure your node by entering a node name and password for administrative access to your node.

.. image:: _images/basic-firstboot.png
   :alt: Setup node at firstboot
   :align: center

Node Name
  Begin the node name with your callsign, followed by unique identifying information of your choice. Node names may contain up to 63 letters, numbers, and dashes, but cannot begin or end with a dash. Underscores, spaces, or any other characters are not allowed. Node names are not case sensitive, but the case will be preserved on the node status display. Amateur radio operators are required to identify all transmitting stations. The AREDN |trade| node name is beaconed automatically by the node every five minutes, so the node name must contain your callsign. Recommended names follow the (callsign)-(label) format, such as AD5BC-MOBILE or AD5BC-120SE. As a general rule node names should be kept as short as possible, while clearly and uniquely identifying the node.

Password
  Set a new administration password for the node with username 'root'. Typically passwords may contain the characters ``a-z``, ``A-Z``, ``0-9``, period ``.``, dash ``-``, underscore ``_``, exclamation ``!``, and tilde ``~``. Avoid linux-reserved characters, including but not limited to ``#``, ``$``, ``&``, ``*``, ``<``, ``>``. Enter your new password again in the *Retype Password* box to verify it is correct. You can click the *eye* icon at the right of the password fields to toggle between hidden and visible text. The first time a node is configured it will require you to change the password. Be sure to remember or record the new password so you can use it for any future administrative tasks on the node.

After providing the new node name and password, click the *Save & Reboot* button. Once your node reboots it will have an IP address in the 10.x.x.x range, so you should set your computer to use `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ to obtain a new IP address from your node. You may need to disconnect/reconnect or disable/enable your computer's Ethernet interface so that it connects using the new IP address. You can open a web browser and enter ``http://localnode.local.mesh`` or ``http://<your-nodename>.local.mesh`` to view the node status page.
