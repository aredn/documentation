=========================
Installing AREDN Firmware
=========================

The steps for installing device firmware are documented on the AREDN |trade| website in the `Current Software <https://www.arednmesh.org/content/current-software>`_ section. Under the **Software** menu, select **Download** to reach the *Current Software* page.

There are two cases for installing AREDN |trade| firmware:

#. If you already have an existing version of AREDN |trade| running on your device, then you can use your computer's web interface to navigate to **Setup** -> **Administration** -> **Firmware Update** to install your new firmware. This process will be explained in more detail in the **Advanced Configuration** section of this guide.

#. If you are installing AREDN |trade| firmware on a device for the first time, each hardware platform may require a unique procedure.

   .. image:: _images/firmware-install.png
      :alt: Firmware Install Connections
      :align: center

   The diagram above shows that your computer with the downloaded firmware image must be connected to the node using Ethernet cables in order to install the AREDN |trade| image. For first-time installs it may be helpful to connect the computer and node through a simple Ethernet switch so that the switch can maintain the computer's link while the node is being rebooted.

   Different node hardware will require different methods for installing the AREDN |trade| firmware. For Ubiquiti devices, your computer's TFTP client will connect to the node's TFTP server in order to upload the firmware image. For TP-LINK devices, your computer's web browser will connect to the node's web server to upload the firmware image. For Mikrotik devices, your computer will run a remote boot server and the node's remote boot client will load its boot image from your computer. Refer to the specific procedures below for your node hardware.

   + **Ubiquiti** devices can typically upload a new firmware image using :abbr:`TFTP (Trivial File Transfer Protocol)`. The up-to-date procedures for accomplishing this task are shown on the `TFTP Firmware Installation <https://www.arednmesh.org/content/tftp-firmware-installation>`_ page of the AREDN |trade| website.

   + **TP-LINK** devices use the manufacturer's pre-installed PharOS interface to upload and apply new firmware images. Navigate to the *Setup* section to select and upload new firmware. Check the TP-LINK documentation for your device if you have questions about using their built-in interface.

   + **Mikrotik** devices can be updated using a specific process that is documented on the `Instructions for Mikrotik Devices <https://www.arednmesh.org/content/installation-instructions-mikrotik-devices>`_ page on the AREDN |trade| website.

----------

Once your device is running AREDN |trade| firmware, you can display its web interface by connecting your computer to the LAN port on the :abbr:`PoE (Power over Ethernet)` and navigating to the following URL: ``http://localnode:8080``

By default AREDN |trade| devices run the :abbr:`DHCP (Dynamic Host Control Protocol)` service on their LAN interface, so your computer will receive an IP address from the node as soon as it is connected with an Ethernet cable. Ensure that your computer is set to obtain its IP address via :abbr:`DHCP (Dynamic Host Control Protocol)`.

.. |trade|  unicode:: U+02122 .. TRADE MARK SIGN
   :ltrim:
