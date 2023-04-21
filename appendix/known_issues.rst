============
Known Issues
============

The following list contains known issues which the development team is aware of and is working to resolve where possible.

Issue #494: Changing the MAC address in the DHCP Reservation may not work.
  *Workaround*: If the IP address you want to change is already in use, then changing the MAC address is not allowed. No workaround at this time.

Issue #142: Changing MESH RF IP Address does not change the corresponding DTD IP address.
  *Workaround*: No workaround at this time.

Issue #49: When a foreign network is attached to the WAN of a mesh node, routing will fail when this network is down.
  *Workaround*: When "Allow others to use my WAN" is enabled, LAN devices and other mesh nodes will continue attempting to route to this down network even though it is unreachable. No workaround at this time.

Issue #41: MikroTik devices not linking over RF on 5MHz channel width.
  *Workaround*: Some models of Mikrotik 2GHz equipment can link with each other but not with other vendor equipment when using 5MHz channel width. This is apparently a hardware issue and can be avoided by using 10MHz channel widths.
