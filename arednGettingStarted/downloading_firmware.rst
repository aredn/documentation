==================================
Downloading AREDN |trade| Firmware
==================================

Current Stable Releases
-----------------------

Once you have selected and obtained a device, the next step is to choose the matching AREDN |trade| firmware image for that specific device. The `AREDN download page <http://downloads.arednmesh.org/firmware/html/stable.html>`_ displays the most current firmware releases for every supported device.

Locate your device model/version in the left column. Most manufacturers print the hardware version on the product package label. In some cases, though, you may need to start the device using the manufacturer's pre-installed firmware and navigate to the system information page to determine the hardware version.

There are two types of firmware images: one for the first-time replacement of the manufacturer's firmware, and the other for upgrades of nodes that are already running AREDN |trade| firmware.

* If you are loading AREDN |trade| firmware on a device for the first time you must download the *factory* firmware from the middle column. For Mikrotik devices you must also download the *sysupgrade* image from the righthand column.

* If you are already running AREDN |trade| firmware on the node then you will choose the *sysupgrade* firmware from the righthand column, and you will use the AREDN |trade| web interface to perform the firmware upgrade.

Once you have selected the correct firmware image for your device, click the link to download the image file to your local computer. Make a note of the download location on your computer, since you will need to use that image to install the AREDN |trade| firmware on your device.

Features Inherited from OpenWRT for New Architectures
  The latest AREDN |trade| firmware contains features which are inherited from the newest OpenWRT upstream release (19.07). The OpenWRT *Release Notes* describe these new features and can be found here: `OpenWRT 19.07 Release Notes <http://openwrt.org/releases/19.07/start>`_

  One important change is the inclusion of a new *target* (architecture) for the firmware, labelled "ath79", which is the successor to the existing "ar71xx" target. The OpenWRT team explains the new target here: `ath79 <https://openwrt.org/docs/techref/targets/ath79>`_. Their main goal is to bring the code into a form that will allow all devices to run a standard unpatched Linux kernel. This will greatly reduce the amount of customization required and will streamline the firmware development process.

  Since not all supported devices have been migrated to the new "ath79" target, AREDN |trade| continues to build firmware for both targets. **You should select the latest recommended target image based on the type of hardware on which it will be installed.** Refer to the latest `firmware notes <http://downloads.arednmesh.org/snapshots/readme.md>`_ in order to ensure you have the correct firmware image for your specific device.

Nightly Build Releases
-----------------------

*Nightly Build* firmware contains the latest bug fixes, features, and support for the newest devices being added to the *Supported Platform Matrix*. It is considered more experimental or cutting-edge firmware. However, if you are having a specific issue that has been addressed in newly developed code, or if you are loading AREDN |trade| firmware onto a device that has just been added, then it might make sense to install the most current *Nightly Build* firmware.

To download the latest build, navigate to the `Software > Nightly Builds <https://www.arednmesh.org/content/nightly-builds>`_ link on the AREDN |trade| website. You will find the most recent *README* file, a list of the latest changes included in the build, and a link to download the firmware. As explained above, select the correct target architecture for the device you will be flashing. To return your device to the current stable release, download the correct *Stable Release* firmware and reflash your device.

*Nightly Build* filenames are prefixed with *aredn-XXXX-yyyyyyy*, where *XXXX* identifies the build number and *yyyyyyy* is a unique software commit identifier. Be aware that as new nightly builds become available, the older builds automatically become obsolete. If you want to install add-on packages for nodes running a nightly build, understand that specific packages may not be available for an *older* build if a *newer* build has already been released. To install packages on nightly build firmware, upgrade to the latest nightly build and then immediately install the packages you desire.
