================================
Video Streaming and Surveillance
================================

The previous section described how audio and video traffic can be transmitted across an AREDN |trade| network to facilitate communication. Since these multimedia streams are supported on mesh networks, you can also use them for many other tasks. One example, `video surveillance <https://en.wikipedia.org/wiki/Closed-circuit_television>`_, is often helpful during an emergency or event and AREDN |trade| networks can be used to deliver this type of traffic to Emergency Operations Centers. Keep in mind that multimedia traffic incurs a much greater cost in terms of network performance and computing resources, so be sure your mesh network is designed with the appropriate bandwidth to handle this traffic.

The photo below shows a Mobile Command Center (MCC) deployed to support a large event in San Juan Capistrano, California. An estimated 35,000 people attend this annual gathering, and the local :abbr:`RACES (Radio Amateur Civil Emergency Service)` team provides realtime video coverage of the parade route for the sheriff’s department and emergency response agencies.

.. image:: _images/eoc-video.png
   :alt: Emergency Operations Center Video
   :align: center

|

More than a dozen high definition `IP cameras <https://en.wikipedia.org/wiki/IP_camera>`_ were collocated at portable AREDN |trade| node sites across the area, and the individual video streams were consolidated on several large displays in the MCC. Orange County Sheriff’s Administrator Sgt. Joseph Cope commented, “This mesh camera system provided by RACES members was a valuable tool for our command staff. The parade was the safest in years. As we were taking the calls, we could see the activity occurring in realtime. Incredibly, there was only one arrest for fighting, which just happened to take place in the camera's view.”

IP Video Cameras
----------------

.. image:: _images/video-surveillance.png
   :alt: Portable Node with Camera
   :align: left

|

IP video cameras may have a fixed direction and focus, or they may be remote controlled `PTZ (Pan, Tilt, Zoom) <https://en.wikipedia.org/wiki/Pan%E2%80%93tilt%E2%80%93zoom_camera>`_ models. The cost and features for video cameras vary widely. On the low end is a very inexpensive Raspberry Pi Zero computer having an integrated camera, shown here next to the Ubiquiti Bullet radio. On the high end are the ruggedized commercial :abbr:`PTZ (Pan, Tilt, Zoom)` cameras which can cost hundreds of dollars, shown here with the bubble dome and infrared LEDs.

Many IP cameras stream video using `Real Time Streaming Protocol (RTSP) <https://en.wikipedia.org/wiki/Real_Time_Streaming_Protocol>`_ in which missing packets are simply skipped during video display. It can be challenging to determine the URL of an RTSP stream, but there is a handy utility at `<https://www.ispyconnect.com/cameras>`_, as well as packet capture utilities such as `Wireshark <https://en.wikipedia.org/wiki/Wireshark>`_, which may help. Frequently a camera supports multiple RTSP URLs each with a different resolution, so you can advertise any of them as a service on an AREDN |trade| node as required. Recently more cameras support `ONVIF (Open Network Video Interface Forum) <https://en.wikipedia.org/wiki/ONVIF>`_, which is a set of protocols and standards that includes RTSP. It supports camera discovery and PTZ camera control.

A 1920x1080 resolution video stream at 60 frames/second can consume up to eight megabits/second of network bandwidth. Few AREDN |trade| networks can consistently support that load, but lower frame rates reduce the required bandwidth proportionally. Typically 720p at 10 frames per second is more than adequate for video surveillance.

IP cameras with an Ethernet port are preferred in order to simplify network connectivity and ensure adequate data transfer speeds. Configure the camera to obtain a mesh IP address from the node, and reserve the address for that camera in the node's DHCP settings so you have a consistent way to connect to it. A camera with :abbr:`PoE (Power over Ethernet)` support is also very useful as this simplifies site cabling.

Some cameras are easier than others to configure and deploy, so be sure to research them carefully before investing in expensive camera hardware.

Video Display Software
----------------------

The software described in this section can help you to provision video surveillance services on your network. The following list is not comprehensive or complete but represents a sample of the types of software that may be available for services on your network. Primarily programs with open source licenses were included in this list, although software with proprietary licenses can also be used successfully.

iSpy
++++

iSpy is a popular video management package for Microsoft Windows computers. It is certified on Windows 7 and above but may work on other systems that support the `.NetV4 Framework <https://en.wikipedia.org/wiki/.NET_Framework>`_. iSpy runs as a Windows program with a local user interface (UI) accessible on the computer on which it was installed. Additional services may be available after paying a subscription fee. Parts of the program are licensed under `LGPLv3 <http://www.gnu.org/licenses/lgpl.html>`_, while other portions are proprietary.

The Windows program provides a "surface" or workspace where you add and configure multiple cameras or microphones. You can then monitor and interact with them to display live video or listen to live audio from network devices. Multimedia streams can be recorded locally for future use, and PTZ cameras can be manipulated with controls in the UI. Motion detection can also be configured, which provides a method for automatically recording multimedia snippets when specific events occur.

iSpy can connect to IP cameras using MJPEG or JPEG sources. It also supports camera connections using MP4, ASF, or RTSP, which it accomplishes through a VLC plugin after `Videolan <http://www.videolan.org/>`_ software is installed. VLC requires usernames and passwords directly in the URL, so you must enter them in clear text as in this example: ``http://admin:password@192.168.1.4/video.asf``.

In the lower right video stream on the iSpy display below you can see the smoke plume from the 2017 `Thomas Fire <https://en.wikipedia.org/wiki/Thomas_Fire>`_ in California, which was recorded by a camera on the local AREDN |trade| network. For additional information about iSpy, visit this link: `iSpy <https://www.ispyconnect.com/>`_.

.. image:: _images/ispy.png
   :alt: iSpy Display
   :align: center

|

MotionEye
+++++++++

MotionEye is a lightweight video display program which runs on Linux and Raspberry Pi computers. It can connect to a variety of USB or IP cameras, and it has the ability to display video streams in a grid format accessible by any web browser on the mesh network. Authentication as a regular user or an administrator will display different menu options: view options for regular users or full administrative control for admin users.

The backend `Motion <https://motion-project.github.io/index.html>`_ engine is built to provide robust motion detection and event triggering. It also enables custom scripts to extend its features, for example to print the system temperature and update it every ten seconds on the display. Many AREDN |trade| operators implement MotionEye on low-power portable Raspberry Pi computers, and the `MotionEyeOS distro <https://github.com/motioneye-project/motioneyeos/wiki>`_ installs the operating system with all dependencies on this platform. For additional information about MotionEye, visit this link: `MotionEye <https://github.com/motioneye-project/motioneye/wiki>`_

.. image:: _images/motioneye.png
   :alt: MotionEye Display
   :align: center

|

ZoneMinder
++++++++++

ZoneMinder is a full-featured video package which runs on Linux computers. Its display is accessible across the mesh network by web browser. IP cameras are supported which use MJPEG streams or an interface to JPEG images. Camera connections can be configured for monitoring, recording, motion detection, or a combination of these.

The ZoneMinder name comes from the fact that it allows administrators to define “zones” or regions of an image, each with different motion detection sensitivity levels. During motion detection, each frame is compared with previous frames and checked for differences. If the amount of change is greater than a specified percentage, an event will be triggered which can capture recordings, send email alerts, or execute external programs. ZoneMinder has extensive features for filtering and comparing video images, which can be useful for monitoring a high traffic area with a single point of interest such as an entry door next to a busy walkway.

This robust feature set comes at the cost of some administrative complexity, making ZoneMinder a good candidate for operators with skills and experience in Linux and video systems. Its open design and the ability to execute external programs makes ZoneMinder very flexible for integration with other systems. For additional information about ZoneMinder, visit this link: `ZoneMinder <https://en.wikipedia.org/wiki/ZoneMinder>`_.

.. image:: _images/zoneminder.png
   :alt: ZoneMinder Display
   :align: center

|

Shinobi
+++++++

Shinobi is a fairly recent video project which implements current methods of streaming for the web. It supports legacy MJPEG/JPEG, FLV, and RTSP streams as well as the newer `HLS <https://en.wikipedia.org/wiki/HTTP_Live_Streaming>`_ and `Websocket <https://en.wikipedia.org/wiki/WebSocket>`_ methods. The web browser interface (UI) is clean and responsive, which renders well on tablets and mobile devices. It is designed for ease of navigation, with dropdown and pop-up menus for snapshots, video recording, event lists, and configuration options.

:abbr:`ONVIF (Open Network Video Interface Forum)` compliance allows Shinobi to provide :abbr:`PTZ (Pan, Tilt, Zoom)` camera controls. Motion detection is accomplished through plugins, with regions configured in the web UI, so if you do not require motion detection you can conserve resources by not adding it to your system. There are three user levels which provide delegation of authority: Superuser, Admin, and Sub-account. Superusers control system settings and create Admin accounts, which control camera settings and manage Sub-accounts and Groups. Sub-accounts have limited privileges and camera profiles can be shared by Group members.

Shinobi tends to conserve computing resources fairly well, so more cameras or higher resolution streams could be supported on a server. The image below shows how motion detection regions are defined, in this case to monitor traffic along an access road to a parking area. For additional information about Shinobi, visit this link: `Shinobi <https://moeiscool.github.io/Shinobi/>`_.

.. image:: _images/shinobi.png
   :alt: Shinobi Display
   :align: center

|

Example Video Service Comparison
--------------------------------

Platform abbreviations:
  win=MS Windows, mac=Apple, lin=Linux, rpi=Raspberry Pi

==========  =================  =============  =============  ======
Program     License            System Load    Platform       Effort
==========  =================  =============  =============  ======
iSpy        freemium           large          windows        easy
MotionEye   open source        medium         lin/rpi        easy
ZoneMinder  open source        large          linux          expert
Shinobi     free for *NC* use  medium         lin/mac        medium
==========  =================  =============  =============  ======

*NC ~ non-commercial*
