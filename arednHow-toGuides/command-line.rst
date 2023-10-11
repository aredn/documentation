================================
Command Line Access to Your Node
================================

There may be times when it would be useful to have command line access to your node. AREDN |trade| nodes support both `Secure Shell (ssh) <https://en.wikipedia.org/wiki/Secure_Shell>`_ and `Telnet <https://en.wikipedia.org/wiki/Telnet>`_. Both access methods will require a set of login credentials (*root* username & password). Linux and MacOS computers have native tools for both *SSH* and *Telnet*.

The *OpenSSH* package can be enabled on Windows computers. Use a web search engine to find information for your specific operating system (for example search "openssh for windows 10"). Here are some examples for enabling OpenSSH on Windows computers:

- `Example for Windows 10 <https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui>`_
- `Example for Windows 11 <https://technoresult.com/how-to-install-and-use-openssh-server-in-windows-11/>`_

On Windows computers you can also use a terminal program such as `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ to connect to your node via ssh or telnet. To learn how to use these programs on your computer, please see the appropriate documentation for the specific programs you have chosen.

As shown in the command line examples below, you begin by opening a terminal window on your computer. At your computer's command prompt, enter the command string you will use to authenticate to your node.

Telnet
  *Telnet* will prompt you for the *root* username and password before displaying your node's command prompt. The *telnet* protocol uses well-known port ``23`` and all traffic is unencrypted. An example *Telnet* command string is

  ::

    $ telnet localnode.local.mesh

  After successfully authenticating, your node's command prompt will be displayed.

  .. image:: _images/telnet-example.png
    :alt:  Telnet example
    :align: center

SSH
  *SSH* requires you to specify the port, *root* username, and password on the command line. This is because AREDN |trade| nodes do not use the default well-known *ssh* port [22], but nodes use port ``2222`` for *ssh* connections. An example *SSH* command string is

  ::

    $ ssh -p 2222 root@localnode.local.mesh

  After successfully authenticating, your node's command prompt will be displayed.

  .. image:: _images/ssh-example.png
    :alt:  SSH example
    :align: center
