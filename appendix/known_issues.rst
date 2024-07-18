============
Known Issues
============

The following list contains known issues which the development team is aware of and is working to resolve where possible.

- Issue #41: MikroTik devices not linking over RF on 5MHz channel width.
  *Workaround*: This is a hardware issue and can be avoided by using 10MHz channel widths.

- Issue #49: When a foreign network is attached to the WAN of a mesh node, routing will fail when this network is down.
  *Workaround*: No workaround at this time.

- Issue #142: Changing MESH RF IP Address does not change the corresponding DTD IP address.
  *Workaround*: No workaround at this time.

- Issue #494: Changing the MAC address in the DHCP Reservation may not work.
  *Workaround*: If the IP address you want to change is already in use, then changing the MAC address is not allowed. No workaround at this time.
