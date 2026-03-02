===================
Custom App Launcher
===================

There may be times when you want to create your own customer application to run on your node, and you would like to include a custom launcher icon in the left nav bar of the web interface. This can be accomplished using the following steps:

1. Create a subdirectory tree under your node's ``/www/`` directory to store your application executable. In the example below the name of the application is ``Performance-Snapshot``, so the directory path will be:

::

  /www/cgi-bin/apps/Performance-Snapshot/

Copy your application executable into this directory and change the filename to ``user`` if you want the launcher to be visible to everyone. If you only want the launcher to be visible when logged in, change the application's filename to ``admin``.

2. Create a subdirectory tree under your node's ``/www/`` directory to store your application's launcher icon (SVG format only). Since the name of the application is ``Performance-Snapshot``, the directory path will be:

::

  /www/apps/Performance-Snapshot/

Copy your application icon into this directory and change the filename to ``icon.svg``.

3. At this point you can reboot your node or simply restart ``uhttpd`` on your node. The new application launcher icon should be visible in the left nav bar, and clicking that icon should open a new browser window or tab for your application to run in.

.. image:: _images/app-launcher.png
   :alt:  Custom app launcher example
   :align: center

Adding an app badge counter and badge-color
-------------------------------------------

You may be implementing an app that is capable of displaying an app badge, for example, a message count on the app icon (as shown in the image above). To display the app counter on the icon, your app must update the ``badge`` file with the appropriate value or count.

1. Create a new subdirectory on your node for the badge data. In this example the name of the application is ``Performance-Snapshot``, so the directory path will be:

::

  /tmp/apps/Performance-Snapshot/

2. Once this directory exists, create a ``badge`` file which your app will update with the latest value or count. In this example, the current value is ``3``.

::

  cat /tmp/apps/Performance-Snapshot/badge
  3

3. If you want to set the color of the badge, you can add a ``badge-color`` file containing the hex color value for displaying the badge. In this example the current badge color value is ``#1E90FF`` (as shown below).

::

  cat /tmp/apps/Performance-Snapshot/badge-color
  #1E90FF
