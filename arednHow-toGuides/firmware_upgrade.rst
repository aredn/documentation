=====================
Firmware Upgrade Tips
=====================

Upgrading an AREDN |trade| node is a straightforward process accomplished using the *Setup > Administration > Firmware Update* feature on the node's web interface. Follow the procedures documented in the **Downloading AREDN Firmware** section to ensure you have the correct firmware version from the AREDN |trade| website to install on your node. The newest firmware versions have a built-in check to verify that the firmware image you selected is appropriate for the device on which you are installing it. Earlier firmware versions (3.16.1.x and 3.18.9.0) do not have these checks, so be sure you selected the correct firmware version for your device before starting the upgrade.

Here are some "best practice" tips to assist with the firmware upgrade process. These ensure that memory utilization is at its minimum on the node. The upgrade process can fail due to lack of memory, but such a failure will leave the node unchanged on its previous firmware version.

Before starting the firmware upgrade, it may be necessary to stop, disable, or uninstall extra packages such as Meshchat, snmp, and tunneling. The goal of this step is to keep those processes from using RAM memory and to free as much RAM as possible before the upgrade. Rebooting the node will ensure that its RAM utilization is at a minimum.

You may also want to stop node programs or services that are not needed during the upgrade. For example, if you can telnet or ssh to the node and type the command ``wifi down`` you can free the memory used by this driver.

When using a web browser to perform an upgrade, be sure to clear the browser's cache to remove any cached pages remaining from your node's previous firmware version. A clear cache will help to eliminate confusion when displaying node data in the browser.

Use a stepped approach to firmware upgrades. For example, if your node is running version 3.18.9.0 you should probably upgrade to version 3.19.3.0 before attempting to apply a newer version.


.. |trade|  unicode:: U+00AE .. Registered Trademark SIGN
   :ltrim:
