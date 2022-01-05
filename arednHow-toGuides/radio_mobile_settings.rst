=========================
Settings for Radio Mobile
=========================

*Contributor: Andre Hansen K6AH*

*Radio Mobile* is a valuable timesaving tool for network planning and modeling. The results obtained depend upon the accuracy of the settings used to generate the model. The following Radio Mobile settings have proven useful. The full AREDN |trade| forum post for these settings appears here: `Radio Mobile Settings <https://www.arednmesh.org/content/question-about-radio-mobile-link>`_

=====================  ===================
Radio System Section   Recommended Setting
=====================  ===================
TX power (Watts)       0.25
TX line loss (dB)      0.5
TX antenna gain (dBi)  [varies]
RX antenna gain (dBi)  [varies]
RX line loss (dB)      0.5
RX threshold (μV)      4
=====================  ===================

While the radio may have a TX Power specification of 1/2 watt (27 dBm), it's more accurate to use 1/4 watt (24 dBm) for dual chain (MIMO) devices because the power is split between the vertical and horizontal domains. The TX and RX Line Loss is minimal, so you can use 1/2 dB to account for the coax jumpers. Using 4 μV for the Receive Threshold will approximate the device's receive sensitivity of -94 dB. It is usually best to underestimate the TX and RX Antenna Gain in order to obtain a more realistic model.

When Radio Mobile completes its link analysis, it will display the Fade Margin.  For a solid connection a fade margin of 15 dB or greater is needed. Anything above that will only increase the MCS rate.  For example, MCS15 requires 19 dB more received signal (94 - 75) and the Ubiquiti Rocket transmit power is 5 dB lower at that same rate, so you will need a total of 24 dB (19 + 5) additional fade margin (39 dB in total) to achieve that data rate. 39 dB is a large Fade Margin and is not often achieved on a link.

**Determining the MCS Rate**

If you telnet to your node, the following command will indicate the MCS rate the device is running:

``cat /sys/kernel/debug/ieee80211/phy0/netdev:wlan0/stations/*/rc_stats``

Here is an example from an endpoint node pointing to a backbone node over 25 miles away. The *Node Status* screen indicates -73/-95/22 dB SNR.

>>>
type         rate     throughput  ewma prob   this prob  retry   this succ/attempt   success    attempts
HT20/LGI     MCS0            5.6      100.0       100.0      1              0(  0)         1           1
HT20/LGI     MCS1           10.5      100.0       100.0      4              0(  0)         4           4
HT20/LGI     MCS2           14.8      100.0       100.0      5              0(  0)        93          93
HT20/LGI     MCS3           18.6       97.7       100.0      5              0(  0)      1380        1416
HT20/LGI  tP MCS4           25.1       99.9       100.0      5              0(  0)     31688       33264
HT20/LGI     MCS5            8.6       25.8       100.0      0              0(  0)       175        3495
HT20/LGI     MCS6            0.0        0.0         0.0      0              0(  0)         1        3495
HT20/LGI     MCS7            0.0        0.0         0.0      0              0(  0)         0        3495
HT20/LGI     MCS8           10.5      100.0       100.0      0              0(  0)         1           1
HT20/LGI     MCS9           18.6       99.9       100.0      5              0(  0)       368         380
HT20/LGI     MCS10          25.1       99.9       100.0      5              0(  0)     37921       38776
HT20/LGI T   MCS11          30.3       99.9       100.0      5              0(  0)    439091      448760
HT20/LGI     MCS12          14.1       33.2       100.0      6              0(  0)      4482        8447
HT20/LGI     MCS13           0.0        0.0         0.0      0              0(  0)         0        3495
HT20/LGI     MCS14           0.0        0.0         0.0      0              0(  0)         0        3496
HT20/LGI     MCS15           0.0        0.0         0.0      0              0(  0)         0        3495

The "T" in the 10th character position indicates the current MCS rate, and a "t" indicates the current fallback rate.  In this case the link is running MCS11 at 30.3 Mbps.
