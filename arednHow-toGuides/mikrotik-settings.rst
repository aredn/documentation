===========================
Help with Mikrotik Settings
===========================

*Contributor: Orv Beach W6BI*

When trying to change the Boot Device to ``try-ethernet-once-then-nand`` you may see the message: "couldn't change settings; not allowed by device-mode." This means the RouterOS *Device Mode* is blocking changes. On recent versions of RouterOS the boot device is controlled by the routerboard Device Mode permission, which is often disabled on home router products such as the hAP ac3, even if the general mode says *advanced*. Enable that capability and physically confirm the change, then set the one-time Etherboot option.

To accomplish this, connect locally with WinBox MAC access, terminal/SSH, or a LAN-side IP to inspect the current permission setting. Note that the device password is located on the pullout tab located on the rear panel.

::

  /system/device-mode/print

If the result includes ``routerboard: no`` then enable it:

::

  /system/device-mode/update mode=advanced routerboard=yes

RouterOS should reply with a prompt similar to:

::

  update: please activate by turning power off or pressing reset or mode button in 5m00s

Within this five-minute window, do one of these while physically at the hAP ac3:

* Briefly press the router's Reset or Mode button, or
* Perform a true cold power-off by unplugging its DC supply or removing PoE power, waiting a few seconds, then restoring power.

Do not use ``/system reboot`` as the confirmation method. The documentation specifically requires a button confirmation or a cold power interruption. This physical step is intended to prevent someone with only remote RouterOS access from quietly enabling sensitive bootloader controls.

After it is back online, verify:

::

  /system/device-mode/print

You should now see:

::

  mode: advanced
  routerboard: yes

Now you can set the boot-device value:

::

  /system/routerboard/settings/set boot-device=try-ethernet-once-then-nand

Finally, reboot or power-cycle the router:

::

  /system/reboot

On its next boot **only**, it will first attempt Etherboot/BOOTP on its Netinstall Ethernet interface. If it does not receive a Netinstall response, it proceeds to NAND and boots RouterOS normally. After this attempt, it returns to normal NAND boot behavior.

Important hAP ac3 details
+++++++++++++++++++++++++

* Use Ethernet 1 for the Netinstall/Etherboot connection.
* Connect it directly to the Netinstall PC or through an uncomplicated Ethernet path; avoid routing, VLANs, Wi-Fi, and potentially interfering DHCP/BOOTP services while troubleshooting.
* Temporarily disable Wi-Fi and other NICs on the Netinstall computer so Netinstall binds to the intended Ethernet adapter.
* The hAP ac3 reset-button recovery procedure can also invoke Netinstall directly: power it up while holding Reset, and release it when the LED turns off-approximately 15 seconds after startup.

Troubleshooting Steps
+++++++++++++++++++++

If the command still fails, check the result of ``/system/device-mode/print`` and look at the results which are displayed:

* If ``routerboard: no`` then RouterBoot is still restricted. Repeat the steps above.

* If ``attempt-count`` is nonzero or you receive “too many unsuccessful attempts” then your Device Mode changes were not confirmed. Cold power-cycle or use the physical power button to confirm and then retry setting ``boot-device`` as shown above.

* If ``routerboard: yes`` but ``protected-routerboot: enabled`` then disable Protected RouterBOOT and retry setting the ``boot-device`` as shown above.
