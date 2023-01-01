==================================
Downloading AREDN |trade| Firmware
==================================

Current Stable Releases
-----------------------

Once you have selected and obtained a device, the next step is to choose the matching AREDN |trade| firmware image for that specific device. The `AREDN download page <http://downloads.arednmesh.org/firmware/html/stable.html>`_ displays the most current firmware releases for every supported device.

Locate your device model/version in the left column. Most manufacturers print the hardware version on the product package label. In some cases, though, you may need to start the device using the manufacturer's pre-installed firmware and navigate to the system information page to determine the hardware version.

There are two types of firmware images: one for the first-time replacement of the manufacturer's firmware, and the other for upgrades of nodes that are already running AREDN |trade| firmware.

- If you are loading AREDN |trade| firmware on TP-LINK or Ubuquiti devices for the first time you must download the *factory* firmware from the middle column. For Mikrotik devices you must download both the *factory* and *sysupgrade* images. For GL.iNet devices you must download the *sysupgrade* image from the righthand column.

- If you are already running AREDN |trade| firmware on the node then you will choose the *sysupgrade* firmware from the righthand column, and you will use the AREDN |trade| web interface to perform the firmware upgrade.

Once you have selected the correct firmware image for your device, click the link to download the image file to your local computer. Make a note of the download location on your computer, since you will need to use that image to install the AREDN |trade| firmware on your device.

Features Inherited from OpenWRT for New Architectures
  The latest AREDN |trade| firmware contains features which are inherited from the newest OpenWRT upstream releases. The `OpenWRT *Release Notes* <https://openwrt.org/>`_ describe these new features. One important change is the inclusion of new *target* architectures for the firmware. The legacy "ar71xx" target has been retired and is replaced by the "ath79" and "ipq40xx" targets.

All supported devices have been migrated to the new targets. **You should select the latest recommended target image based on the type of hardware on which it will be installed.** Refer to the latest `Supported Devices <http://downloads.arednmesh.org/snapshots/SUPPORTED_DEVICES.md>`_ in order to ensure you have the correct firmware image for your specific device.

Nightly Build Firmware
-----------------------

*Nightly Build* firmware contains the latest bug fixes, features, and support for the newest devices being added to the *Supported Platform Matrix*. It allows the wider mesh community to test new code before it is included in a formal code release. The Nightly Build is considered more experimental or cutting-edge and may not be suitable for *production* nodes. However, if you are having a specific issue that has been addressed in newly developed code, or if you are loading AREDN |trade| firmware onto a device that has just been added, then it might make sense to install the nightly build firmware.

To download the *Nightly Build*, navigate to the `Software > Nightly Builds <https://www.arednmesh.org/content/nightly-builds>`_ link on the AREDN |trade| website. Nightly Build filenames are prefixed with *aredn-XXXX-yyyyyyy*, where *XXXX* identifies the build number and *yyyyyyy* is a unique software commit identifier. You will find the most recent *README* file, a cumulative list of the changes included in the *CHANGELOG*, the most recent list of *SUPPORTED_DEVICES*, and a link to download the firmware. As explained above, select the correct target and subtarget for the device you will be flashing. To return your device to the current stable release, download the correct *Stable Release* firmware and reflash your device.

Be aware that when a new nightly build becomes available, any older builds automatically become obsolete. If you want to install add-on packages for nodes running a nightly build, understand that specific packages will not be available for an *older* build if a *newer* build has superseded it. Be sure to upgrade to the current nightly build before installing packages. Nightly build firmware contains the cumulative changes that have gone before, so review the *Changelog* to determine which features are included in the build.
