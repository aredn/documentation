=================================
Installing AREDN |trade| Firmware
=================================

There are two cases for installing AREDN |trade| firmware:

1. If you already have an existing version of AREDN |trade| running on your device, then you can use your computer's web browser and navigate to **Setup > Administration > Firmware Update** to install your new firmware. This process will be explained in more detail in the **Configuration Deep Dive** section of this guide. Also, see *Firmware Upgrade Tips* in the **How-to Guides** section for additional information.

2. If you are installing AREDN |trade| firmware on a device for the first time, each hardware platform may require a unique procedure.

.. image:: _images/firmware-install.png
  :alt: Firmware Install Connections
  :align: center

The diagram above shows that your computer with the downloaded firmware image must be connected to the node using Ethernet cables in order to install the AREDN |trade| image. It is helpful to connect the computer and node through a simple Ethernet switch so that the switch can maintain the computer's network link even when the node is rebooting.

Different node hardware will require different methods for installing the AREDN |trade| firmware. For **Ubiquiti** devices, your computer's `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_ client will connect to the node's TFTP server in order to upload the firmware image. For **Mikrotik** and **TP-LINK** devices, your computer will run a `PXE <https://en.wikipedia.org/wiki/Preboot_Execution_Environment>`_ server and the node's remote boot client will download the boot image from your computer. For **GL-iNet** devices, your computer's web browser will connect to the node's web server to upload the firmware image. Refer to the specific procedures below for your node hardware.

If you experience an issue uploading firmware to your device you can refer to the *Firmware Tips* document in the **How-To Guide**.

Firmware First Install Checklists
---------------------------------

It may be helpful to have a brief checklist of steps to follow when doing the initial firmware installation on node hardware. The checklists below are provided to assist with this process, based on the manufacturer of your device. Complete step-by-step instructions are detailed in the sections that follow.

:download:`GL.iNet First Install Checklist (PDF) <_images/GL.iNet_First_Install_Checklist.pdf>`

:download:`Mikrotik First Install Checklist (PDF) <_images/Mikrotik_First_Install_Checklist.pdf>`

:download:`TP-LINK First Install Checklist (PDF) <_images/TP-LINK_First_Install_Checklist.pdf>`

:download:`Ubiquiti First Install Checklist (PDF) <_images/Ubiquiti_First_Install_Checklist.pdf>`

Ubiquiti First Install Process
------------------------------

Ubiquiti devices have a built-in `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_ *server* to which you can upload the AREDN |trade| *factory* image. Your computer must have **TFTP client** software available. Linux and Mac both have native TFTP clients, but you may need to enable or obtain a TFTP client for Windows computers. If you are using a Windows computer, use a web search engine to find information for your specific version (for example search "tftp client for windows 10"). There is a wealth of information available online for configuring your computer with a TFTP client program.

Different TFTP client programs may have different command line options or flags that must be used, so be sure to study the command syntax for your TFTP client software. The example shown below may not include the specific options required by your client program.

Download the appropriate *factory* file for your device by following the instructions in the **Downloading AREDN Firmware** section of this documentation.

1. Set your computer’s Ethernet network adapter to a static IP address that is a member of the correct subnet for your device. Check the documentation for your specific hardware to determine the correct network number. As in the example below, most Ubiquiti devices have a default IP address of 192.168.1.20, so you can give your computer a static IP on the 192.168.1.x network with a netmask of 255.255.255.0. For example, set your Ethernet adapter to a static IP address of 192.168.1.100.

  You can choose any number for the fourth octet, as long as it is not the same as the IP address of the node. Of course you must also avoid using 192.168.1.0 and 192.168.1.255, which are reserved addresses that identify the network itself and the broadcast address for that network. Other devices may have different default IP addresses or subnets, so select a static IP for your computer which puts it on the same subnet but does not conflict with the default IP of the device.

2. Connect an Ethernet cable from your computer to the dumb switch, and another cable from the LAN port of the PoE adapter to the switch.

3. Put the Ubiquiti device into TFTP mode by holding the reset button while plugging your node's Ethernet cable into the *POE* port on the PoE adapter. Continue holding the device's reset button for approximately 30 to 45 seconds until you see the LEDs on the node alternating in a 1-3, 2-4, 1-3, 2-4 pattern, then release the reset button.

4. Open a command window on your computer and execute a file transfer command to send the AREDN firmware to your device. Target the default IP address of your Ubiquiti node, such as 192.168.1.20 or 192.168.1.1 for AirRouters. The following is one example of TFTP commands that transfer the firmware image to a node:

  >>>
  [Linux/Mac]
  > tftp 192.168.1.20
  > bin                 [Transfer in "binary" mode]
  > trace on            [Show the transfer in progress]
  > put <full path to the firmware file>
    [For example, put /temp/aredn-<release>-factory.bin]
  -----------------------------------
  [Windows with command on a single line]
  > tftp.exe -i 192.168.1.20 put C:\temp\aredn-<release>-factory.bin

  The TFTP client should indicate that data is being transferred and eventually completes.

5. Watch the LEDs for about 2-3 minutes until the node has finished rebooting. The reboot is completed when the LED 4 light (farthest on the right) is lit and is steady green.

6. Configure your computer’s Ethernet network interface to use DHCP for obtaining an IP address from the node. You may need to unplug/reconnect the Ethernet cable from your computer to force it to get a new IP address from the node.

7. After the node reboots, open a web browser and use either ``http://192.168.1.1`` or ``http://localnode.local.mesh`` for the URL. Some computers may have DNS search paths configured that require you to use the `fully qualified domain name (FQDN) <https://en.wikipedia.org/wiki/Fully_qualified_domain_name>`_ to resolve *localnode* to the mesh node's IP address.

8. Click the *Setup* button and configure the new “firstboot” node as described in the **Basic Radio Setup** section.

Mikrotik First Install Process
------------------------------

Mikrotik devices require a **two-part install** process: First, boot the correct mikrotik-vmlinux-initramfs file with the **elf** extension, and then use that temporary AREDN |trade| Administration environment to complete the installation of the appropriate *sysupgrade* file with the **bin** extension.

Mikrotik devices have a built-in `PXE <https://en.wikipedia.org/wiki/Preboot_Execution_Environment>`_ client which allows them to download a boot image from an external source. Your computer must run a **PXE Server** to provide an IP address and boot image to Mikrotik devices. The important functions of a **PXE** server are to give the node an IP address via `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ as well as providing the firmware image via `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_. The reason AREDN |trade| suggests using the 192.168.1.x network on your **PXE** server is to eliminate the need to change IP addresses on your computer during the install process. AREDN |trade| firmware uses the 192.168.1.x network once it is loaded, so using it all the way through the process will simplify things for you.

Preparation
  - Download *both* of the appropriate Mikrotik *factory* and *sysupgrade* files from the AREDN |trade| website. Rename the **elf** file to ``rb.elf`` and keep the *sysupgrade* **bin** file available for later.

  - Set your computer’s Ethernet network adapter to a static IP address on the subnet you will be using for the new device. This can be any network number of your choice, but it is recommended that you use the 192.168.1.x subnet because it will put devices on the network you will eventually need to use in order to complete the installation. For example, you can give your computer a static IP such as 192.168.1.100 with a netmask of 255.255.255.0. You can choose any number for the fourth octet, as long as it is not within the range of DHCP addresses you will be providing as shown below.

  - Connect an Ethernet cable from your computer to the network switch, and another cable from the LAN port of the PoE adapter to the switch. Finally connect an Ethernet cable from the *POE* port to the node, but leave the device powered off for now. If you are flashing a *Mikrotik hAP ac lite* that uses a separate AC adapter, connect the last Ethernet cable from the switch to the Mikrotik's WAN port (1).

PXE Boot: *Linux Procedure*
  1. Create a directory on your computer called ``/tftp`` and copy the ``rb.elf`` file there.

  2. Determine your computer’s Ethernet *interface name* with ``ifconfig``. It will be the interface you set to 192.168.1.100 above. You will use this interface name in the command below as the name after ``-i`` and you must substitute your login user name after ``-u`` below. Use a ``dhcp-range`` of IP addresses that are also on the same subnet as the computer: for example 192.168.1.110,192.168.1.120 as shown below.

  3. Open a terminal window to execute the following dnsmasq command with escalated privileges:

      >>>
      > sudo dnsmasq -i eth0 -u joe --log-dhcp --bootp-dynamic --dhcp-range=192.168.1.110,192.168.1.120 -d -p0 -K --dhcp-boot=rb.elf --enable-tftp --tftp-root=/tftp/

  4. With the unit powered off, press and hold the reset button on the radio while powering on the device. Continue to hold the reset button until you see output information from the computer window where you ran the dnsmasq command, which should happen after 20-30 seconds. Release the reset button when you see the "sent" message, which indicates success, and you can now <ctrl>-C or end dnsmasq.

  5. The node will now automatically reboot with the temporary AREDN |trade| Administration image.

PXE Boot: *Windows Procedure*
  You will need to install and configure a `PXE <https://en.wikipedia.org/wiki/Preboot_Execution_Environment>`_ Server on your Windows computer. The example below uses *Tiny PXE* which can be downloaded from `erwan.labalec.fr <https://erwan.labalec.fr/tinypxeserver/>`_. There may be other alternative Windows programs that accomplish the same goal, such as `ERPXE <https://erpxe.com/>`_ or `Serva <https://www.vercot.com/~serva/>`_.

  1. Navigate to the folder where you extracted the *Tiny PXE* software and edit the ``config.ini`` file.  Directly under the ``[dhcp]`` tag, add the following line: ``rfc951=1`` then save and close the file.

  2. Copy the ``rb.elf`` file into the ``files`` folder under the *Tiny PXE* server directory location.

  3. Start the *Tiny PXE* server exe and select your computer's Ethernet IP address from the dropdown list called ``Option 54 [DHCP Server]``, making sure to check the ``Bind IP`` checkbox. Under the "Boot File" section, enter ``rb.elf`` into the the *Filename* field, and uncheck the checkbox for "Filename if user-class = gPXE or iPXE". Click the *Online* button at the top of the *Tiny PXE* window.

  .. image:: _images/tiny-pxe-mik.png
    :alt: Tiny PXE Display for Mikrotik
    :align: center

  4. With the unit powered off, press and hold the reset button on the node while powering on the device. Continue holding the reset button until you see ``TFTPd: DoReadFile: rb.elf`` in the *Tiny PXE* log window.

  5. Release the node’s reset button and click the *Offline* button in *Tiny PXE*. You are finished using *Tiny PXE* when the **elf** image has been read by the node.

  6. The node will now automatically reboot with the temporary AREDN |trade| Administration image.

Install the *sysupgrade* Firmware Image
  1. After booting the **elf** image the node will have a default IP address of 192.168.1.1. Your computer should already have a static IP address on this subnet, but if not then give your computer an IP address on this subnet.

    .. attention:: For the *Mikrotik hAP ac lite* **only**, disconnect the Ethernet cable from the WAN port (1) on the Mikrotik and insert it into one of the LAN ports (2,3,4) before you proceed.

    You should be able to ping the node at 192.168.1.1. Don't proceed until you can ping the node. You may need to disconnect and reconnect your computer's network cable to ensure that your IP address has been reset. Also, you may need to clear your web browser's cache in order to remove cached pages remaining from your node's previous firmware version.

  2. In a web browser, open the node’s Administration page ``http://192.168.1.1/cgi-bin/admin`` (user = 'root', password = 'hsmm') and immediately navigate to the *Firmware Update* section. Browse to find the *sysupgrade* **bin** file you previously downloaded and click the *Upload* button.

      As an alternative to using the node's web interface, you can manually copy the *sysupgrade* **bin** file to the node and run a command line program to install the firmware. This will allow you to see any error messages that may not appear when using the web interface. Note that devices running AREDN |trade| firmware images use port 2222 for secure copy/shell access.

      Execute the following commands from a Linux computer:

      >>>
      my-computer:$ scp -P 2222 <aredn-firmware-filename>.bin root@192.168.1.1:/tmp
      my-computer:$ ssh -p 2222 root@192.168.1.1
      ~~~~~~~ after logging into the node with ssh ~~~~~~~
      node:# sysupgrade -n /tmp/<aredn-firmware-filename>.bin

      To transfer the image from a Windows computer you can use a *Secure Copy* program such as `WinSCP <https://winscp.net>`_. Then use a terminal program such as `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ to connect to the node via ssh or telnet in order to run the sysupgrade command shown as the last line above.

  3. The node will now automatically reboot with the new AREDN |trade| firmware image.

TP-LINK First Install Process
-----------------------------

**TP-LINK** devices may or may not allow you to use the manufacturer's pre-installed *PharOS* web browser interface to apply new firmware images. If available, this is the most user-friendly way to install AREDN |trade| firmware. Navigate to the system setup menu to select and upload new firmware. Check the TP-LINK documentation for your device if you have questions about using their built-in user interface. If this process works then you will have AREDN |trade| firmware installed on your device and you do not need to follow any of the steps described below.

If the process above does not work or if you choose not to use the *PharOS* web interface, then you can install AREDN |trade| firmware on your device using steps similar to those described above for Mikrotik devices. TP-LINK devices have a built-in `PXE <https://en.wikipedia.org/wiki/Preboot_Execution_Environment>`_ client which allows them to obtain new firmware from an external source. Your computer must run a **PXE Server** to provide an IP address and boot image to the device. The important functions of a **PXE** server are to give the node an IP address via `DHCP <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>`_ as well as providing the firmware image via `TFTP <https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol>`_. The reason AREDN |trade| suggests using the 192.168.1.x network on your **PXE** server is to eliminate the need to change IP addresses on your computer during the install process. AREDN |trade| firmware uses the 192.168.1.x network once it is loaded, so using it all the way through the process will simplify things for you.

Preparation
  - Download the appropriate TP-LINK *factory* file and rename this file as ``recovery.bin``

  - Set your computer’s Ethernet network adapter to a static IP address on the subnet you will be using for the new device. This can be any network number of your choice, but it is recommended that you use the 192.168.1.x subnet because it will put devices on the network you will eventually need to use to complete the installation. For example, you can give your computer a static IP such as 192.168.1.100 with a netmask of 255.255.255.0. You can choose any number for the fourth octet, as long as it is not within the range of DHCP addresses you will be providing as shown below.

  - Connect an Ethernet cable from your computer to the network switch, and another cable from the LAN port of the PoE adapter to the switch. Finally connect an Ethernet cable from the *POE* port to the node, but leave the device powered off for now.

Linux Procedure
  1. Create a directory on your computer called ``/tftp`` and copy the TP-LINK ``recovery.bin`` file there.

  2. Determine your computer’s Ethernet interface name with ``ifconfig``. It will be the interface you set to 192.168.1.100 above. You will use this interface name in the command below as the name after ``-i`` and you must substitute your login user name after ``-u`` below. Use a ``dhcp-range`` of IP addresses that are also on the same subnet as the computer: for example 192.168.1.110,192.168.1.120 as shown below.

  3. Open a terminal window to execute the following dnsmasq command with escalated privileges:

      >>>
      > sudo dnsmasq -i eth0 -u joe --log-dhcp --bootp-dynamic --dhcp-range=192.168.1.110,192.168.1.120 -d -p0 -K --dhcp-boot=recovery.bin --enable-tftp --tftp-root=/tftp/

  4. With the unit powered off, press and hold the reset button on the radio while powering on the device. Continue to hold the reset button until you see output information from the computer window where you ran the dnsmasq command, which should happen after 20-30 seconds. Release the reset button when you see the "sent" message, which indicates success, and you can now <ctrl>-C or end dnsmasq.

  5. The node will now automatically reboot with the new AREDN |trade| firmware image.

Windows Procedure
  You will need to install and configure a `PXE <https://en.wikipedia.org/wiki/Preboot_Execution_Environment>`_ Server on your Windows computer. The example below uses *Tiny PXE* which can be downloaded from  `erwan.labalec.fr <https://erwan.labalec.fr/tinypxeserver/>`_. There may be other alternative Windows programs that accomplish the same goal, such as `ERPXE <https://erpxe.com/>`_ or `Serva <https://www.vercot.com/~serva/>`_.

  1. Navigate to the folder where you extracted the *Tiny PXE* software and edit the ``config.ini`` file.  Directly under the ``[dhcp]`` tag, add the following line:  ``rfc951=1`` then save and close the file.

  2. Copy the ``recovery.bin`` firmware image into the ``files`` folder under the *Tiny PXE* server directory location.

  3. Start the *Tiny PXE* server exe and select your computer's Ethernet IP address from the dropdown list called ``Option 54 [DHCP Server]``, making sure to check the ``Bind IP`` checkbox. Under the "Boot File" section, enter ``recovery.bin`` into the the *Filename* field, and uncheck the checkbox for "Filename if user-class = gPXE or iPXE". Click the *Online* button at the top of the *Tiny PXE* window.

  .. image:: _images/tiny-pxe-tpl.png
    :alt: Tiny PXE Display for TP_LINK
    :align: center

  4. With the unit powered off, press and hold the reset button on the node while powering on the device. Continue holding the reset button until you see ``TFTPd: DoReadFile: recovery.bin`` in the *Tiny PXE* log window.

  5. Release the node’s reset button and click the *Offline* button in *Tiny PXE*. You are finished using *Tiny PXE* when the firmware image has been read by the node.

  6. The node will now automatically reboot with the new AREDN |trade| firmware image.

GL-iNet First Install Process
------------------------------

**GL-iNet** devices allow you to use the manufacturer's pre-installed *OpenWRT* web interface to upload and apply new firmware images. Check the GL-iNet documentation for your device if you have questions about initial configuration. Both GL-iNet and AREDN |trade| devices provide DHCP services, so you should be able to connect your computer and automatically receive an IP address on the correct subnet. GL-iNet devices usually have a default IP address of 192.168.8.1, so if for some reason you need to give your computer a static IP address you can use that subnet.

After the GL-iNet device is first booted and configured, navigate to the **Upgrade** section and click *Local Upgrade* to select the AREDN |trade| *sysupgrade.bin* file you downloaded for your device.

.. attention:: Be sure to uncheck the **Keep Settings** checkbox, since GL.iNet settings are incompatible with AREDN |trade| firmware.

The node will automatically reboot with the new AREDN |trade| firmware image. If for some reason your GL-iNet device gets into an unusable state, you should be able to recover using the process documented here:
`GL-iNet debrick procedure <https://docs.gl-inet.com/en/2/troubleshooting/debrick/>`_

After the Firmware Install
--------------------------

After the node reboots, it should have a default IP address of 192.168.1.1. By default AREDN |trade| devices provide :abbr:`DHCP (Dynamic Host Control Protocol)` on their LAN interface, so your computer will receive an IP address automatically from the node. Ensure that your computer is set to obtain its IP address via :abbr:`DHCP (Dynamic Host Control Protocol)`.

You should be able to ping the node at 192.168.1.1. Don't proceed until you can ping the node. You may need to disconnect and reconnect your computer's network cable to ensure that your IP address has been reset.

Once your device is running AREDN |trade| firmware, you can display its web interface by navigating to either ``http://192.168.1.1`` or ``http://localnode.local.mesh``. You may need to clear your web browser's cache in order to remove any cached pages. You can use your web browser to configure the new node with your callsign, admin password, and other settings as described in the **Basic Radio Setup** section of the documentation.
