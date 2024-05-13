:original_name: ALM-12045.html

.. _ALM-12045:

ALM-12045 Read Packet Dropped Rate Exceeds the Threshold
========================================================

Description
-----------

The system checks the read packet dropped rate every 30 seconds. This alarm is generated when the read packet dropped rate exceeds the threshold (the default threshold is 0.5%) for multiple times (the default value is **5**).

To change the threshold, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Dropped Rate**.

This alarm is cleared when **Trigger Count** is 1 and the read packet dropped rate is less than or equal to the threshold. This alarm is cleared when **Trigger Count** is greater than 1 and the read packet dropped rate is less than or equal to 90% of the threshold.

The alarm detection is disabled by default. If you want to enable this function, check whether this function can be enabled based on Checking System Environments.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12045    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------+
| Name              | Meaning                                                           |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| PortName          | Specifies the network port for which the alarm is generated.      |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The service performance deteriorates or some services time out.

Risk warning: In SUSE kernel 3.0 or later or Red Hat 7.2, the system kernel modifies the mechanism for counting the number of dropped read packets. In this case, this alarm may be generated even if the network is running properly, but services are not affected. You are advised to check the system environment first.

Possible Causes
---------------

-  An OS exception occurs.
-  The NICs are bonded in active/standby mode.
-  The alarm threshold is improperly configured.
-  The network quality is poor.

Procedure
---------

**View the network packet dropped rate.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm, and view the name of the host for which the alarm is generated and the NIC name.

#. Log in to the alarm node as user **omm**, and run the **/sbin/ifconfig** *NIC name* command to check whether packet loss occurs on the network.

   |image2|

   .. note::

      -  *IP address of the node for which the alarm is generated*: Query the IP address of the node for which the alarm is generated on the **Hosts** page of MRS Manager based on the value of **HostName** in the alarm location information. Check both the IP addresses of the management plane and service plane.
      -  Packet loss rate = (Number of dropped packets/Total number of received packets) x 100%. If the packet loss rate is greater than the system threshold (0.5% by default), read packets are dropped.

   -  If yes, go to :ref:`11 <alm-12045__li4196511811134>`.
   -  If no, go to :ref:`3 <alm-12045__li6542838717657>`.

**Check the system environment.**

3. .. _alm-12045__li6542838717657:

   Log in to the active OMS node or the alarm node as user **omm**.

4. Run the **cat /etc/*-release** command to check the OS type.

   -  For Red Hat Enterprise Linux, go to :ref:`5 <alm-12045__li5563721171656>`.

      .. code-block::

         # cat /etc/*-release
         Red Hat Enterprise Linux Server release 7.2 (Santiago)

   -  For SUSE Linux, go to :ref:`6 <alm-12045__li42309040172040>`.

      .. code-block::

         # cat /etc/*-release
         SUSE Linux Enterprise Server 11 (x86_64)
         VERSION = 11
         PATCHLEVEL = 3

   -  For other OS types, go to :ref:`11 <alm-12045__li4196511811134>`.

5. .. _alm-12045__li5563721171656:

   Run the **cat /etc/redhat-release** command to check whether the OS version is **Red Hat 7.2 (x86)** or **Red Hat 7.4 (TaiShan)**.

   .. code-block::

      # cat /etc/redhat-release
      Red Hat Enterprise Linux Server release 7.2 (Santiago)

   -  If yes, the alarm sending function cannot be enabled. Go to :ref:`7 <alm-12045__li43950618195120>`.
   -  If no, go to :ref:`11 <alm-12045__li4196511811134>`.

6. .. _alm-12045__li42309040172040:

   Run the **cat /proc/version** command to check whether the SUSE kernel version is 3.0 or later.

   .. code-block::

      # cat /proc/version
      Linux version 3.0.101-63-default (geeko@buildhost) (gcc version 4.3.4 [gcc-4_3-branch revision 152973] (SUSE Linux) ) #1 SMP Tue Jun 23 16:02:31 UTC 2015 (4b89d0c)

   -  If yes, the alarm sending function cannot be enabled. Go to :ref:`7 <alm-12045__li43950618195120>`.
   -  If no, go to :ref:`11 <alm-12045__li4196511811134>`.

7. .. _alm-12045__li43950618195120:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Threshold Configuration**.

8.  In the navigation tree of the **Thresholds** page, choose *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Dropped Rate**. In the area on the right, check whether the **Switch** is toggled on.

    -  If yes, the alarm sending function is enabled. Go to :ref:`9 <alm-12045__li38517503111027>`.
    -  If no, the alarm sending function is disabled. Go to :ref:`10 <alm-12045__li16613085112024>`.

9.  .. _alm-12045__li38517503111027:

    In the area on the right, toggle **Switch** off to disable the checking of **Network Read Packet Dropped Rate Exceeds the Threshold**.

    |image3|

10. .. _alm-12045__li16613085112024:

    On the **Alarm** page of MRS Manager, search for alarm **12045** and manually clear the alarm if it is not automatically cleared. No further action is required.

    |image4|

    .. note::

       ID of the Network Read Packet Dropped Rate Exceeds the Threshold alarm is **12045**.

**Check whether the NICs are bonded in active/standby mode.**

11. .. _alm-12045__li4196511811134:

    Log in to the alarm node as user **omm** and run the **ls -l /proc/net/bonding** command to check whether the **/proc/net/bonding** directory exists on the node.

    -  If yes, the bond mode is configured for the node. Go to :ref:`12 <alm-12045__li56651960171744>`.

       .. code-block::

          # ls -l /proc/net/bonding/
          total 0
          -r--r--r-- 1 root root 0 Oct 11 17:35 bond0

    -  If no, the bond mode is not configured for the node. Go to :ref:`14 <alm-12045__li61276131112834>`.

       .. code-block::

          # ls -l /proc/net/bonding/
          ls: cannot access /proc/net/bonding/: No such file or directory

12. .. _alm-12045__li56651960171744:

    Run the **cat /proc/net/bonding/**\ *bond0* command to check whether the value of **Bonding Mode** in the configuration file is **fault-tolerance**.

    .. note::

       In the command, **bond0** indicates the name of the bond configuration file. Use the file name obtained in :ref:`11 <alm-12045__li4196511811134>`.

    .. code-block::

       # cat /proc/net/bonding/bond0
       Ethernet Channel Bonding Driver: v3.7.1 (April 27, 2011)

       Bonding Mode: fault-tolerance (active-backup)
       Primary Slave: eth1 (primary_reselect always)
       Currently Active Slave: eth1
       MII Status: up
       MII Polling Interval (ms): 100
       Up Delay (ms): 0
       Down Delay (ms): 0

       Slave Interface: eth0
       MII Status: up
       Speed: 1000 Mbps
       Duplex: full
       Link Failure Count: 1
       Slave queue ID: 0

       Slave Interface: eth1
       MII Status: up
       Speed: 1000 Mbps
       Duplex: full
       Link Failure Count: 1
       Slave queue ID: 0

    -  If yes, the NICs are bonded in active/standby mode. Go to :ref:`13 <alm-12045__li44376005172456>`.
    -  If no, go to :ref:`14 <alm-12045__li61276131112834>`.

13. .. _alm-12045__li44376005172456:

    Check whether the NIC specified by **NetworkCardName** in the alarm is the standby NIC.

    -  If yes, the alarm of the standby NIC cannot be automatically cleared. Manually clear the alarm on the alarm management page. No further action is required.
    -  If no, go to :ref:`14 <alm-12045__li61276131112834>`.

       .. note::

          To determine the standby NIC, check the **/proc/net/bonding/bond0** configuration file. If the NIC name corresponding to **NetworkCardName** is **Slave Interface** but not **Currently Active Slave** (the current active NIC), the NIC is the standby one.

**Check whether the threshold is set properly.**

14. .. _alm-12045__li61276131112834:

    Log in to MRS Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Dropped Rate**, and check whether the alarm threshold is configured properly. The default value is **0.5%**. You can adjust the threshold as needed.

    -  If yes, go to :ref:`17 <alm-12045__li56023883112834>`.
    -  If no, go to :ref:`15 <alm-12045__li47653126112834>`.

15. .. _alm-12045__li47653126112834:

    Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Dropped Rate**. Click **Modify** in the **Operation** column to change the threshold. See :ref:`Figure 1 <alm-12045__fig52784093112834>`.

    .. _alm-12045__fig52784093112834:

    .. figure:: /_static/images/en-us_image_0000001582927657.png
       :alt: **Figure 1** Configuring the alarm threshold

       **Figure 1** Configuring the alarm threshold

16. After 5 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`17 <alm-12045__li56023883112834>`.

**Check whether the network connection is normal.**

17. .. _alm-12045__li56023883112834:

    Contact the network administrator to check whether the network is normal.

    -  If yes, rectify the fault and go to :ref:`18 <alm-12045__li4503547112834>`.
    -  If no, go to :ref:`19 <alm-12045__li40531926112834>`.

18. .. _alm-12045__li4503547112834:

    After 5 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-12045__li40531926112834>`.

**Collect the fault information.**

19. .. _alm-12045__li40531926112834:

    On MRS Manager of the active cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

20. Select **OMS** for **Service** and click **OK**.

21. Expand the **Hosts** dialog box and select the alarm node and the active OMS node.

22. Click |image5| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

23. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087417.png
.. |image2| image:: /_static/images/en-us_image_0000001532767498.png
.. |image3| image:: /_static/images/en-us_image_0000001532607762.png
.. |image4| image:: /_static/images/en-us_image_0000001532448274.png
.. |image5| image:: /_static/images/en-us_image_0000001532927350.png
