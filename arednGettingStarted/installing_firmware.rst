=================================
Installing AREDN |trade| Firmware
=================================

There are two cases for installing AREDN |trade| firmware:

1. If you already have an existing version of AREDN |trade| running on your device, then you can use your computer's web interface to navigate to **Setup > Administration > Firmware Update** to install your new firmware. This process will be explained in more detail in the **Advanced Configuration** section of this guide. Also, see *Firmware Upgrade Tips* in the **How-to Guides** section for additional information.

2. If you are installing AREDN |trade| firmware on a device for the first time, each hardware platform may require a unique procedure.

.. image:: _images/firmware-install.png
  :alt: Firmware Install Connections
  :align: center

The diagram above shows that your computer with the downloaded firmware image must be connected to the node using Ethernet cables in order to install the AREDN |trade| image. It is helpful to connect the computer and node through a simple Ethernet switch so that the switch can maintain the computer's network link while the node is being rebooted.

Different node hardware will require different methods for installing the AREDN |trade| firmware. For **Ubiquiti** devices, your computer's `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_ client will connect to the node's TFTP server in order to upload the firmware image. For **Mikrotik** and **TP-LINK** devices, your computer will run a remote boot server and the node's remote boot client will load its boot image from your computer. For **GL-iNet** devices, your computer's web browser will connect to the node's web server to upload the firmware image. Refer to the specific procedures below for your node hardware.

Troubleshooting Tips
--------------------

Questions and troubleshooting assistance can usually be obtained by creating a post on the AREDN |trade| `online forum <https://www.arednmesh.org/forum>`_, which has an active community of helpful and experienced operators.

Browser cache and sessions
  One common issue can occur when installing firmware using a web browser interface. Your computer's web browser cache stores data for the URLs that have been visited, but IP addresses and other parameters often change during the install process. It is possible for the cache to contain information that doesn’t match the latest settings for the URL, so the browser may block the connection setup and display an ERR_CONNECTION_RESET message. Clearing your computer's web browser cache will allow the latest URL settings to be registered so you can continue with the install process.

  Instead of a *Connection Reset* message, sometimes a *Bad Gateway* message may appear. This is an `HTTP Status Code <https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml>`_ that can mean any of several things. Often it indicates a network communication issue between a web browser and a web server. During AREDN |trade| firmware installs you can usually resolve a *Bad Gateway* issue by doing one or more of the following things:

  * Refresh or Reload the URL for your node.
  * Clear your browser cache and delete cookies.
  * Close your browser and restart a new session.
  * Use a different web browser program or a *Safe Mode / Incognito* browser window.
  * Unplug and reconnect the Ethernet cable from your computer to ensure that your machine has received a new DHCP IP address on the same subnet as the node's updated IP.

PXE Server
  If you are using a TFTP/Bootp server (described below) on a Windows computer, be sure to allow the Tiny PXE server through the Windows firewall when prompted on first launch. If you are not prompted or the Tiny PXE server does not display any activity when you put your device in recovery mode, go to the firewall settings from the Windows control panel and click *Advanced Settings*. Look through the "Inbound Rules" to see if a rule exists for Tiny PXE server. If a rule exists, make sure to "allow connection" for both private and public networks. If no rule exists, create a new rule allowing connection for both public and private networks.

Ubiquiti First Install Process
------------------------------

**Ubiquiti** devices have a built-in `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_ server to which you can upload the AREDN |trade| *factory* image. Your computer must have TFTP client software available. Linux and Mac both have native TFTP clients, but you may need to enable or obtain a TFTP client for Windows computers. If you are using a Windows computer, `enable the TFTP client <https://www.trishtech.com/2014/10/enable-tftp-telnet-in-windows-10/>`_ or download and install another `standalone TFTP client <https://www.tftp-server.com/tftp-client.html>`_ of your choice.

Different TFTP client programs may have different command line options or flags that must be used, so be sure to study the command syntax for your TFTP client software. The example shown below may not include the specific options required by your client program.

Download the appropriate *factory* file for your device by following the instructions in the **Downloading AREDN Firmware** section of this documentation.

1. Set your computer’s Ethernet network adapter to a static IP address that is a member of the correct subnet for your device. Check the documentation for your specific hardware to determine the correct network number. As in the example below, most Ubiquiti devices have a default IP address of 192.168.1.20, so you can give your computer a static IP on the 192.168.1.x network with a netmask of 255.255.255.0. For example, set your Ethernet adapter to a static IP address of 192.168.1.100.

  You can choose any number for the fourth octet, as long as it is not the same as the IP address of the node. Of course you must also avoid using 192.168.1.0 and 192.168.1.255, which are reserved addresses that identify the network itself and the broadcast address for that network. Other devices may have different default IP addresses or subnets, so select a static IP for your computer which puts it on the same subnet but does not conflict with the default IP of the device.

2. Connect an Ethernet cable from your computer to the dumb switch, and another cable from the LAN port of the PoE adapter to the switch.

3. Put the Ubiquiti device into TFTP mode by holding the reset button while plugging your node's Ethernet cable into the POE port on the PoE adapter. Continue holding the device's reset button for approximately 30 to 45 seconds until you see the LEDs on the node alternating in a 1-3, 2-4, 1-3, 2-4 pattern, then release the reset button.

4. Open a command window on your computer and execute a file transfer command to send the AREDN firmware to your device. Target the default IP address of your Ubiquiti node, such as 192.168.1.20 or 192.168.1.1 for AirRouters. The following is one example of TFTP commands that transfer the firmware image to a node:

  >>>
  [Linux/Mac]
  > tftp 192.168.1.20
  > bin                 [Transfer in "binary" mode]
  > trace on            [Show the transfer in progress]
  > put <full path to the firmware file>
    [For example, put /temp/aredn-3.19.3.0-ubnt-nano-m-xw-factory.bin]
  -----------------------------------
  [Windows with command on a single line]
  > tftp -i 192.168.1.20 put C:\temp\aredn-3.19.3.0-ubnt-nano-m-xw-factory.bin

  The TFTP client should indicate that data is being transferred and eventually completes.

5. Watch the LEDs for about 2-3 minutes until the node has finished rebooting. The reboot is completed when the LED 4 light (farthest on the right) is lit and is steady green.

6. Configure your computer’s Ethernet network interface to use DHCP for obtaining an IP address from the node. You may need to unplug/reconnect the Ethernet cable from your computer to force it to get a new IP address from the node.

7. After the node reboots, open a web browser and use either ``http://192.168.1.1`` or ``http://localnode.local.mesh`` for the URL. Some computers may have DNS search paths configured that require you to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ to resolve *localnode* to the mesh node's IP address.

8. Click the *Setup* button and configure the new “firstboot” node as described in the **Basic Radio Setup** section.

Mikrotik First Install Process
------------------------------

Mikrotik devices require a **two-part install** process: First, install and boot the correct mikrotik-vmlinux-initramfs file with the **elf** extension, and then use this temporary AREDN |trade| Administration display to complete the installation of the appropriate mikrotik-rb file with the **bin** extension.

Mikrotik devices have a built-in :abbr:`TFTP (Trivial File Transfer Protocol)` and `Bootp <https://en.wikipedia.org/wiki/Bootstrap_Protocol>`_ client which allows them to obtain new firmware from an external source. Your computer must run a TFTP/Bootp *server* (described below) in order to provide firmware images to Mikrotik devices.

Preparation
  1. Download the appropriate Mikrotik **elf** and **bin** files. Rename the *elf* file to ``rb.elf`` and keep the *bin* file available for later.

  2. Set your computer’s Ethernet network adapter to a static IP address that is a member of the correct subnet for your device. Check the documentation for your specific hardware to determine the correct network number. As in the example below, most Mikrotik devices use the 192.168.1.x subnet by default, so you can give your computer a static IP such as 192.168.1.100 with a netmask of 255.255.255.0.

    You can choose any number for the fourth octet, as long as it is not the same as the IP address of the node and is not within the range of DHCP addresses you will be providing in step 2 below. Of course you must also avoid using 192.168.1.0 and 192.168.1.255, which are reserved addresses that identify the network itself and the broadcast address for that network. Other devices may use different default subnets, such as QRT units which use 192.168.88.x. Select a static IP for your computer which puts it on the same subnet as your device.

  3. Connect an Ethernet cable from your computer to the dumb switch, and another cable from the LAN port of the PoE adapter to the switch. If you are flashing a *Mikrotik hAP ac lite* device, connect the Ethernet cable from *Port #1* of the Mikrotik to the dumb switch.

Linux Procedure
  1. Create a directory on your computer called ``/tftp`` and copy the ``rb.elf`` file there.

  2. Determine your computer’s Ethernet interface name with ``ifconfig``. It will be the interface you set to 192.168.1.100 above. You will use this interface name in the command below as the name after ``-i`` and you must substitute your login user name after ``-u`` below. Use a ``dhcp-range`` of IP addresses that are also on the same subnet as the computer: for example 192.168.1.110,192.168.1.120 as shown below.

  3. Become ``root`` and open a terminal window to execute the following dnsmasq command:

      >>>
      (root)# dnsmasq -i eth0 -u joe --log-dhcp --bootp-dynamic \
        --dhcp-range=192.168.1.110,192.168.1.120 -d -p0 -K \
        --dhcp-boot=rb.elf --enable-tftp --tftp-root=/tftp/

  4. With the PoE unit powered off, connect the Mikrotik node to the POE port. If you are flashing a Mikrotik *hAP ac lite* device, connect the LAN cable from *Port 1* of the Mikrotik to the dumb switch. Press and hold the reset button on the Mikrotik while powering on the device.

  5. Continue to hold the reset button until you see output information from the computer window where you ran the dnsmasq command, which should happen after about ten seconds. Release the reset button as the computer starts communicating with the node. When you see the "sent" message, this indicates success, and the node has downloaded the image and will reboot. You can now <ctrl>-C or kill dnsmasq.

Windows Procedure
  You will need `Tiny PXE <http://reboot.pro/files/file/303-tiny-pxe-server/>`_ software on your Windows computer. Download this software and extract it on your computer.

  1. Navigate to the folder where you extracted the *Tiny PXE* software and edit the ``config.ini`` file.  Directly under the ``[dhcp]`` tag, add the following line:  ``rfc951=1`` then save and close the file.

  2. Copy the ``rb.elf`` file into the ``files`` folder under the Tiny PXE server directory location.

  3. Start the Tiny PXE server exe and select your Ethernet interface IP from the dropdown list called ``Option 54 [DHCP Server]``, making sure to check the ``Bind IP`` checkbox. Under the "Boot File" section, enter ``rb.elf`` into the the *Filename* field, and uncheck the checkbox for "Filename if user-class = gPXE or iPXE". Click the *Online* button at the top of the Tiny PXE window.

  .. image:: _images/tiny-pxe-mik.png
    :alt: Tiny PXE Display for Mikrotik
    :align: center

  4. With the PoE unit powered off, connect the Mikrotik node to the POE port. If you are flashing a Mikrotik *hAP ac lite* device, connect the LAN cable from *Port 1* of the Mikrotik to the dumb switch.

  5. Press and hold the reset button on the node while powering on the PoE unit or the device. Continue holding the reset button until you see ``TFTPd: DoReadFile: rb.elf`` in the Tiny PXE log window.

  6. Release the node’s reset button and click the *Offline* button in Tiny PXE. You are finished using Tiny PXE when the firmware image has been read by the node.

Final Configuration Steps
  1. After booting the AREDN firmware image the node should have a default IP address of 192.168.1.1. Change your computer’s Ethernet interface to DHCP mode to obtain an IP address from the node.

    .. attention:: For the *Mikrotik hAP ac lite* **only**, pull the Ethernet cable from the WAN port (1) on the Mikrotik and insert it into one of the LAN ports (2,3,4) before you proceed.

    You should be able to ping the node at 192.168.1.1. Don't proceed until you can ping the node. You may need to disconnect and reconnect your computer's network cable to ensure that your IP address has been reset. Also, you may need to clear your web browser's cache in order to remove cached pages remaining from your node's previous firmware version.

  2. In a web browser, open the node’s Administration page ``http://192.168.1.1/cgi-bin/admin`` (user = 'root', password = 'hsmm') and navigate to the *Setup > Administration > Firmware Update* section. Select the **bin** file you previously downloaded and click the *Upload* button. After uploading the **bin** file, the node will automatically reboot.

      As an alternative to using the node's web interface, you can manually copy the **bin** file to the node and run a command line program to install the image. This will allow you to see any error messages that may not appear when using the web interface. Note that AREDN |trade| nodes use port 2222 for secure copy/shell access.

      Execute the following commands from a Linux computer:

      >>>
      my-computer:$ scp -P 2222 aredn-firmware-filename.bin root@192.168.1.1:/tmp
      my-computer:$ ssh -p 2222 root@192.168.1.1
      ~~~~~~~ after logging into the node with ssh ~~~~~~~
      node:# sysupgrade -n /tmp/aredn-firmware-filename.bin

      To transfer the image from a Windows computer you can use a *Secure Copy* program such as `WinSCP <https://winscp.net>`_. Then use a terminal program such as `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ to connect to the node via ssh or telnet in order to run the sysupgrade command shown as the last line above.

  3. After the node reboots, navigate to the node’s *Setup* page and configure the new “firstboot” node as described in the **Basic Radio Setup** section.

TP-LINK First Install Process
-----------------------------

**TP-LINK** devices may or may not allow you to use the manufacturer's pre-installed *PharOS* web browser interface to apply new firmware images. If available, this is the most user-friendly way to install AREDN |trade| firmware. Navigate to the system setup menu to select and upload new firmware. Check the TP-LINK documentation for your device if you have questions about using their built-in user interface. If this process works then you will have AREDN |trade| firmware installed on your device and you do not need to follow any of the steps described below.

If the process above does not work or if you choose not to use the *PharOS* web interface, then you can always install AREDN |trade| firmware on your device using the following steps. TP-LINK devices have a built-in :abbr:`TFTP (Trivial File Transfer Protocol)` and `Bootp <https://en.wikipedia.org/wiki/Bootstrap_Protocol>`_ client which allows them to obtain new firmware from an external source. Your computer must run a TFTP/Bootp *server* (described below) in order to provide firmware images to the device.

Preparation
  1. Download the appropriate TP-LINK *factory* file and rename this file as ``recovery.bin``

  2. Set your computer’s Ethernet network adapter to a static IP address that is a member of the correct subnet for your device. Check the documentation for your specific hardware to determine the correct network number. As in the example below, most TP-LINK devices use the 192.168.0.x subnet by default, so you can give your computer a static IP such as 192.168.0.100 with a netmask of 255.255.255.0.

    You can choose any number for the fourth octet, as long as it is not the same as the IP address of the node and is not within the range of DHCP addresses you will be providing in step 2 below. Of course you must also avoid using 192.168.0.0 and 192.168.0.255, which are reserved addresses that identify the network itself and the broadcast address for that network. Other devices may have different default IP addresses or subnets, so select a static IP for your computer which puts it on the same subnet.

  3. Connect an Ethernet cable from your computer to the dumb switch, and another cable from the LAN port of the PoE adapter to the switch.

Linux Procedure
  1. Create a directory on your computer called ``/tftp`` and copy the TP-LINK ``recovery.bin`` file there.

  2. Determine your computer’s Ethernet interface name with ``ifconfig``. It will be the interface you set to 192.168.0.100 above. You will use this interface name in the command below as the name after ``-i`` and you must substitute your login user name after ``-u`` below. Use a ``dhcp-range`` of IP addresses that are also on the same subnet as the computer: for example 192.168.0.110,192.168.0.120 as shown below.

  3. Become ``root`` and open a terminal window to execute the following dnsmasq command:

      >>>
      (root)# dnsmasq -i eth0 -u joe --log-dhcp --bootp-dynamic \
        --dhcp-range=192.168.0.110,192.168.0.120 -d -p0 -K \
        --dhcp-boot=recovery.bin --enable-tftp --tftp-root=/tftp/

  4. With the PoE unit powered off, connect an Ethernet cable from the TP-LINK node to the POE port.

  5. Push the reset button on the TP-LINK and hold it while powering on the PoE unit.  Continue to hold the reset button until you see output information from the computer window where you ran the dnsmasq command, which should happen after about 10 seconds.  Release the reset button as the computer starts communicating with the node.  When you see the "sent" message, this indicates success, and the TP-LINK node has downloaded the image and will reboot. You can now <ctrl>-C or kill dnsmasq.

Windows Procedure
  You will need `Tiny PXE <http://reboot.pro/files/file/303-tiny-pxe-server/>`_ software on your Windows computer. Download this software and extract it on your computer.

  1. Navigate to the folder where you extracted the *Tiny PXE* software and edit the ``config.ini`` file.  Directly under the ``[dhcp]`` tag, add the following line:  ``rfc951=1`` then save and close the file.

  2. Copy the ``recovery.bin`` firmware image into the ``files`` folder under the Tiny PXE server directory location.

  3. Start the Tiny PXE server exe and select your Ethernet interface IP from the dropdown list called ``Option 54 [DHCP Server]``, making sure to check the ``Bind IP`` checkbox. Under the "Boot File" section, enter ``recovery.bin`` into the the *Filename* field, and uncheck the checkbox for "Filename if user-class = gPXE or iPXE". Click the *Online* button at the top of the Tiny PXE window.

  .. image:: _images/tiny-pxe-tpl.png
    :alt: Tiny PXE Display
    :align: center

  4. With the PoE unit powered off, connect an Ethernet cable from the TP-LINK node to the POE port. Press and hold the reset button on the node while powering on the PoE unit. Continue holding the reset button until you see ``TFTPd: DoReadFile: recovery.bin`` in the Tiny PXE log window.

  5. Release the node’s reset button and click the *Offline* button in Tiny PXE. You are finished using Tiny PXE when the firmware image has been read by the node.

Final Configuration Steps
  1. Configure your computer’s Ethernet network interface to use DHCP for obtaining an IP address from the node. You may need to disconnect and reconnect your computer's network cable to ensure that your IP address has been reset.

  2. After the node reboots, open a web browser and enter the following URL: ``http://localnode.local.mesh``  Some computers may have DNS search paths configured that require you to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ to resolve *localnode* to the mesh node's IP address.

  3. Navigate to the *Setup* page and configure the new “firstboot” node as described in the **Basic Radio Setup** section.

GL-iNet First Install Process
------------------------------

**GL-iNet** devices allow you to use the manufacturer's pre-installed *OpenWRT* web interface to upload and apply new firmware images. Check the GL-iNet documentation for your device if you have questions about initial configuration. Both GL-iNet and AREDN |trade| devices provide DHCP services, so you should be able to connect your computer and automatically receive an IP address on the correct subnet. GL-iNet devices usually have a default IP address of 192.168.8.1, so if for some reason you need to give your computer a static IP address you can use that subnet.

After the GL-iNet device has been booted and configured, navigate to the *Upgrade* section and click *Local Upgrade* to select the AREDN |trade| "sysupgrade.bin" file you downloaded for your device.

.. attention:: Be sure to uncheck the **Keep Settings** checkbox, since GL.iNet settings are incompatible with AREDN |trade| firmware.

After the device has rebooted to the AREDN |trade| image, you should be able to ping the device at 192.168.1.1 and navigate to ``http://192.168.1.1`` to continue with the firstboot or NOCALL settings process. If for some reason your GL-iNet device gets into an unusable state, you should be able to recover using the process documented here:
`GL-iNet debrick procedure <https://docs.gl-inet.com/en/2/troubleshooting/debrick/>`_

Post-Install Steps
------------------

Once your device is running AREDN |trade| firmware, you can display its web interface by connecting your computer to the LAN port on the :abbr:`PoE (Power over Ethernet)` and navigating to either ``http://192.168.1.1`` or ``http://localnode.local.mesh``. Some computers may have DNS search paths configured that require you to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ to resolve *localnode* to the mesh node's IP address. Each node will serve its web interface on both port 80 and 8080.

By default AREDN |trade| devices run the :abbr:`DHCP (Dynamic Host Control Protocol)` service on their LAN interface, so your computer will receive an IP address from the node as soon as it is connected with an Ethernet cable. Ensure that your computer is set to obtain its IP address via :abbr:`DHCP (Dynamic Host Control Protocol)`. You may also need to clear your web browser's cache in order to remove cached pages remaining from your node's previous firmware version.

.. |trade|  unicode:: U+00AE .. Registered Trademark SIGN
   :ltrim:
