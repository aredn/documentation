==================================
Downloading AREDN |trade| Firmware
==================================

Once you have selected and obtained a device, the next step is to choose the matching AREDN |trade| firmware image for that specific device. The `AREDN download page <http://downloads.arednmesh.org/firmware/html/stable.html>`_ displays the most current firmware releases for every supported device.

Locate your device model/version in the left column. Most manufacturers print the hardware version on the product package label. In some cases, though, you may need to start the device using the manufacturer's pre-installed firmware and navigate to the system information page to determine the hardware version.

There are two types of firmware images: one for the first-time replacement of the manufacturer's firmware, and the other for upgrades of nodes that are already running AREDN |trade| firmware.

* If you are loading AREDN |trade| firmware on a device for the first time you must download the *factory* firmware from the middle column. For Mikrotik devices you must also download the *sysupgrade* image from the righthand column.

* If you are already running AREDN |trade| firmware on the node then you will choose the *sysupgrade* firmware from the righthand column, and you will use the AREDN |trade| web interface to perform the firmware upgrade.

Once you have selected the correct firmware image for your device, click the link to download the image file to your local computer. Make a note of the download location on your computer, since you will need to use that image to install the AREDN |trade| firmware on your device.

Features Inherited from OpenWRT for New Architectures
  The latest AREDN |trade| firmware contains features which are inherited from the newest OpenWRT upstream release (19.07). The OpenWRT *Release Notes* describe these new features and can be found here: `OpenWRT 19.07 Release Notes <http://openwrt.org/releases/19.07/start>`_

  One important change is the inclusion of a new *target* (architecture) for the firmware, labelled "ath79", which is the successor to the existing "ar71xx" target. The OpenWRT team explains the new target here: `ath79 <http://openwrt.org/docs/techref/targets/ath79>`_. Their main goal is to bring the code into a form that will allow all devices to run a standard unpatched Linux kernel. This will greatly reduce the amount of customization required and will streamline the firmware development process.

  Since not all supported devices have been migrated to the new "ath79" target, AREDN |trade| continues to build firmware for both targets. **You should select the latest recommended target image based on the type of hardware on which it will be installed.** Refer to the latest `firmware notes <http://downloads.arednmesh.org/snapshots/trunk/readme.md>`_ in order to ensure you have the correct firmware image for your specific device.


.. |trade|  unicode:: U+00AE .. Registered Trademark SIGN
   :ltrim:
