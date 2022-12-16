============
Known Issues
============

The following list contains known issues which the development team is aware of and is working to resolve where possible.

Issue #497: Channel 6 does not work for the LAN AP with 2GHz radio.
  *Workaround*: Avoid channel 6 for LAN AP with 2 GHz radio.

Issue #494: Changing the MAC address in the DHCP Reservation may not work.
  *Workaround*: If the IP address you want to change is already in use, then changing the MAC address is not allowed. No workaround at this time.

Issue #414: WiFi Scan shows bogus channels.
  *Workaround*: This appears to occur when collocated nodes are running at high power. Apparently the baseband signal of the chip may be getting detected at times and reported to random channels. Since this situation does not cause any RF issues it can be ignored, or you can shield or reduce power on the devices to remove the bogus entries from the scan list.

Issue #352: Legacy SSH rsa key issue.
  Newer applications have begun deprecating ssh-rsa keys, which are used on AREDN nodes.

  .. attention:: This issue has been resolved in the 3.22.12.0 firmware release.

  *Workaround*: Try explicitly identifying the key type to your application, for example:

  ``ssh -oHostKeyAlgorithms=+ssh-rsa -p 2222 root@myNode.local.mesh``

Issue #142: Changing MESH RF IP Address does not change the corresponding DTD IP address.
  *Workaround*: No workaround at this time.

Issue #49: When a foreign network is attached to the WAN of a mesh node, routing will fail when this network is down.
  *Workaround*: When "Allow others to use my WAN" is enabled, LAN devices and other mesh nodes will continue attempting to route to this down network even though it is unreachable. No workaround at this time.

Issue #41: MikroTik devices not linking over RF on 5MHz channel width.
  *Workaround*: Some models of Mikrotik 2GHz equipment can link with each other but not with other vendor equipment when using 5MHz channel width. This is apparently a hardware issue and can be avoided by using 10MHz channel widths.
