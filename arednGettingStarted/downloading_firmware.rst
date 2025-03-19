==================================
Downloading AREDN® Firmware
==================================

Types of Firmware
-----------------

**Stable Release** firmware has been tested and shown to work on the devices that were supported at the time of the release. This firmware is considered to be stable and suitable for production devices deployed in the field. Stable Release firmware is identified by numbers such as ``3.25.2.0``. In this example ``25.2`` indicates the year (2025) and month (Feb) of the release.

**Nightly Build** firmware contains the latest bug fixes, features, and support for new devices. It allows the wider mesh community to test new code before it is included in a Stable Release. The Nightly Build is considered more experimental or cutting-edge and may not be suitable for production nodes. However, it might make sense to install the Nightly Build if you are having a specific issue that has been addressed in newly developed code or if you are loading AREDN® firmware onto a device that is newly supported. The Nightly Build filename shows the build date and the software commit identifier for that specific firmware build. Be aware that when a new nightly build appears, any older builds automatically become obsolete. If you want to install add-on packages for nodes running a nightly build, understand that specific packages are not available for an *older* build if a *newer* build has superseded it. Be sure to upgrade to the current nightly build before installing packages.

Choosing Firmware to Download
-----------------------------

The first step is to choose the AREDN® firmware image for your specific hardware. You can find the available firmware images for your device by using the `AREDN® Firmware Selector (AFS) <http://downloads.arednmesh.org/afs/www/>`_.

.. image:: _images/afs-1.png
   :alt: AREDN Firmware Selector
   :align: center

Enter the first few characters of the hardware manufacturer in the *Model* search field (case insensitive), then click the firmware image dropdown on the right to choose the firmware release that you want to download. Next, find your device model in the search results list and click the row for your hardware. As shown below, this display will have links for all of the firmware images that are available to download for your device.

.. image:: _images/afs-2.png
   :alt: AREDN Firmware Selector
   :align: center

|

There are usually two types of firmware images shown for each device: one for the first-time replacement of the manufacturer's firmware, and the other for upgrades of nodes that are already running AREDN® firmware.

TP-LINK or Ubiquiti
  If you are loading firmware on TP-LINK or Ubuquiti devices for the first time you must download the *FACTORY* firmware. Otherwise download the *SYSUPGRADE* firmware image.

Mikrotik
  If you are loading firmware on Mikrotik devices for the first time you must download **both** the *KERNEL* and *SYSUPGRADE* images. Otherwise download only the *SYSUPGRADE* firmware image.

  As noted in the Mikrotik install instructions, if you determine that your device is running RouterOS ``v7.x`` you can try to install the *SYSUPGRADE-V7* image or you can follow the procedure to downgrade RouterOS and then install the regular *SYSUPGRADE* image.

GL.iNET and OpenWRT One
  For these devices you will only see the *SYSUPGRADE* image for both first-time installs and firmware upgrades.

Click the appropriate button to download the image file to your local computer. Make a note of the download location on your computer, since you will use the downloaded image(s) to install the AREDN® firmware on your device.

Features Inherited from OpenWRT for New Architectures
  The latest AREDN® firmware contains features which are inherited from the newest OpenWRT upstream releases. The `OpenWRT *Release Notes* <https://openwrt.org/>`_ describe these new features. One important change is the inclusion of new *target* architectures for the firmware. The legacy "ar71xx" target has been retired and is replaced by the "ath79" and "ipq40xx" targets.

  All supported devices have been migrated to the new targets. **You should select the latest recommended target image based on the type of hardware on which it will be installed.** Refer to the latest `Supported Devices <http://downloads.arednmesh.org/snapshots/SUPPORTED_DEVICES.md>`_ in order to ensure you have the correct firmware image for your specific device.
