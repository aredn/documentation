========================
Virtual Machine Installs
========================

*Contributor: Trevor Raty KG6MDW*

The use of virtual machines as AREDN |trade| nodes is for advanced users. Most users should use *Mikrotik ac2* or *ac3* hardware to achieve similar functionality. These instructions are provided with the assumption that you understand your virtualization platform and are familiar with creating images and uploading virtual disks. The x86_64 image has been tested and is considered stable on the Proxmox, Unraid, and VMware ESXi platforms, so usage on other virtualization platforms may not work as expected.

In order to have the most current features, it is recommended that you install a Nightly Build image of the AREDN |trade| firmware. For example, there is a known issue in the x86_64 firmware before 3.23.12.0 when using more than one Ethernet interface, but this was resolved in subsequent releases.

Prerequisites / Image information
---------------------------------

At a minimum the VM must have two virtual CPUs, 64mb memory, and approximately 200mb free storage. Providing more CPU is generally not needed on modern hardware. Extra memory can be useful for a Supernode or large tunnel server, however more than 1gb is not needed.

There are two modes for networking: single-port and multi-port. This is automatically selected based on the number of available network interfaces detected. Set the number of interfaces *before* powering on the VM for the first time.

Single-port mode
  All traffic utilizes VLANs as described in the *Node VLANs* section of the **Configuration Deep Dive** documentation. This requires your virtual interface to be VLAN aware or to be set as a passthrough interface.

Multi-port mode
  Ports can be assigned as needed to be LAN, DtD or WAN links. If your virtual interface is VLAN aware, you can tag VLANs; otherwise the interface should be untagged, which is the recommended setting. In this mode the following ports are automatically assigned:

  - First interface: WAN
  - Second interface: DtD
  - Third and beyond: LAN

.. note:: The images do not include any *vmtools* but they do contain drivers for the standard QEMU/VMware paravirtualized storage and networking. Using the paravirtualized devices is recommended.

QEMU Install Process
--------------------

1. Download the latest firmware image from the AREDN |trade| downloads website.

2. Extract the .gz file. *7zip* on Windows may have issues with the .gz file, so you may need to download *gzip* for Windows or extract it on a Linux or Mac computer/VM.

3. Upload/copy the ``.img`` file to your VM server. You can rename the image if you desire.

4. Create the VM/Domain on your server and assign the ``.img`` file to it.

5. Boot the VM and proceed with the AREDN |trade| node configuration steps.

VMware Install Process
----------------------

For VMware you will need to use QEMU tools or another V2V converter in order to convert the image to ``vmdk`` format. Some example software is listed below:

- `QEMU for Windows binaries (Unoffical) <https://qemu.weilnetz.de/w64/>`_
- `QEMU Official downloads <https://www.qemu.org/download/#windows>`_
- `Starwind Converter <https://www.starwindsoftware.com/starwind-v2v-converter>`_

1. Download the latest firmware image from the AREDN |trade| downloads website.

2. Extract the .gz file. *7zip* on Windows may have issues with the .gz file, so you may need to download *gzip* for Windows or extract it on a Linux or Mac computer/VM.

3. Convert the ``.img`` to ``.vmdk`` using your V2V converter of choice. For example, if you are using QEMU, open a terminal/command prompt and on Windows navigate to where QEMU is installed (normally ``c:\Program Files\qemu\``). Run the following command, replacing "aredn.vmdk" and "aredn.img" with the filenames you have chosen.

::

  qemu-img convert -f raw -O vmdk aredn.img aredn.vmdk

If you are using Virtualbox, below is the built-in command, replacing "aredn.vmdk" and "aredn.img" with the filenames you have chosen.

::

  VBoxManage internalcommands createrawvmdk -filename aredn.vmdk -rawdisk aredn.img

4. Create the VM/Domain on your server, but *do not assign it a disk*.

5. Upload/copy the ``.vmdk`` file to your server. You can rename the image if you desire.

6. ``ssh`` to the ESXi host, navigate to where the ``.vmdk`` file was uploaded and run the following command to verify/fix any conversion issues. This step helps to identify and fix potential image errors.

::

  vmkfstools -i uploaded.vmdk verified.vmdk

7. Assign the verified ``.vmdk`` disk to the VM.

8. Boot the VM and proceed with the AREDN |trade| node configuration steps.
