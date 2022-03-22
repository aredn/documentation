=====================
Firmware Upgrade Tips
=====================

Upgrading an AREDN |trade| node is a straightforward process accomplished using the *Setup > Administration > Firmware Update* feature on the node's web interface. Follow the procedures documented in the **Downloading AREDN Firmware** section to ensure you have the correct firmware version from the AREDN |trade| website to install on your node

Here are some "best practice" tips to assist with the firmware upgrade process. These ensure that memory utilization is at its minimum on the node. The upgrade process can fail due to lack of memory, but such a failure will leave the node running its previous firmware version.

Clear the web browser cache
  When using a web browser to perform an upgrade, be sure to clear the browser's cache to remove any cached pages remaining from your node's previous firmware version. A clear cache will help to eliminate confusion when displaying node data in the browser.

Release node resources
  Before starting the firmware upgrade on low memory devices, it may be necessary to stop, disable, or uninstall extra packages such as Meshchat, snmp, and tunneling. The goal of this step is to keep those processes from using RAM memory and to free as much RAM as possible before the upgrade. Rebooting the node before beginning the upgrade will ensure that RAM utilization is at a minimum.

  You may also want to stop node programs or services that are not needed during the upgrade. For example, you can telnet or ssh to the node and type the command ``wifi down`` to free the memory used by this driver.

Tips for legacy nodes with low memory (32mb)
  Legacy equipment with only 32mb of memory may require more effort to upgrade as the footprint of firmware images continues to grow. Be sure not to use these types of devices at sites which are difficult to access. The sysupgrade process needs around 10mb of free memory to succeed.

  * You may need to try the sysupgrade procedure several times before it succeeds. Be patient and keep trying.

  * Get everything ready to do the upgrade, then do a fresh reboot of the node and immediately start the sysupgrade process before the node has time to initialize services which use memory.

  * Use command line access to copy the *sysupgrade.bin* image to the /tmp directory on the node, then run the sysupgrade process manually from the command line on the node. Note that AREDN |trade| nodes use port 2222 for secure copy and secure shell access.

    Execute the following commands from a Linux computer:

    >>>
    my-computer:$ scp -P 2222 aredn-firmware-filename.bin root@192.168.1.1:/tmp
    my-computer:$ ssh -p 2222 root@192.168.1.1
    ~~~~~~~ after logging into the node with ssh ~~~~~~~
    node:# sysupgrade -n /tmp/aredn-firmware-filename.bin

    To transfer the image from a Windows computer you can use a *Secure Copy* program such as `WinSCP <https://winscp.net>`_. Then use a terminal program such as `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ to connect to the node via ssh or telnet in order to run the sysupgrade command shown as the last line above.

  * As a last resort, use the TFTP procedure to load the *factory.bin* firmware image to the node. This procedure is described in the *First Install* sections of **Installing AREDN Firmware**.
