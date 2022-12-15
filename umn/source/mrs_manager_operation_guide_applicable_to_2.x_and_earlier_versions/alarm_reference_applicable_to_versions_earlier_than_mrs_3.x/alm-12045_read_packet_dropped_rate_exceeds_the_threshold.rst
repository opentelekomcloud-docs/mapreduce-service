:original_name: alm_12045.html

.. _alm_12045:

ALM-12045 Read Packet Dropped Rate Exceeds the Threshold
========================================================

Description
-----------

The system checks the read packet dropped rate every 30 seconds. This alarm is generated when the read packet dropped rate exceeds the threshold (the default threshold is 0.5%) for multiple times (the default value is **5**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Network Reading** > **Network Read Packet Rate Information** > **Read Packet Dropped Rate**.

This alarm is cleared when **hit number** is 1 and the read packet dropped rate is less than or equal to the threshold. This alarm is cleared when **hit number** is greater than 1 and the read packet dropped rate is less than or equal to 90% of the threshold.

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

+-------------------+--------------------------------------------------------------+
| Parameter         | Description                                                  |
+===================+==============================================================+
| ServiceName       | Specifies the service for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.         |
+-------------------+--------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.         |
+-------------------+--------------------------------------------------------------+
| NetworkCardName   | Specifies the network port for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

The service performance deteriorates or some services time out.

Risk warning: In SUSE kernel 3.0 or later or Red Hat 7.2, the system kernel modifies the mechanism for counting the number of dropped read packets. In this case, this alarm may be generated even if the network is running properly, but services are not affected. You are advised to check the system environment first.

Possible Causes
---------------

-  An OS exception occurs.
-  The NICs are bonded in active/standby mode.
-  The alarm threshold is improperly configured.
-  The network environment is abnormal.

Procedure
---------

**View the network packet dropped rate.**

#. Use PuTTY to log in to any non-alarm node in the cluster as user **omm** and run the **ping** *IP address of the node for which the alarm is generated* **-c 100** command to check whether packet drop occurs on the network.

   .. code-block::

      # ping 10.10.10.12 -c 5
      PING 10.10.10.12 (10.10.10.12) 56(84) bytes of data.
      64 bytes from 10.10.10.11: icmp_seq=1 ttl=64 time=0.033 ms
      64 bytes from 10.10.10.11: icmp_seq=2 ttl=64 time=0.034 ms
      64 bytes from 10.10.10.11: icmp_seq=3 ttl=64 time=0.021 ms
      64 bytes from 10.10.10.11: icmp_seq=4 ttl=64 time=0.033 ms
      64 bytes from 10.10.10.11: icmp_seq=5 ttl=64 time=0.030 ms
      --- 10.10.10.12 ping statistics ---
      5 packets transmitted, 5 received, 0% packet loss, time 4001ms   rtt min/avg/max/mdev = 0.021/0.030/0.034/0.006 ms

   .. note::

      -  *IP address of the node for which the alarm is generated*: Query the IP address of the node for which the alarm is generated on the node management page of the MRS cluster details page based on the value of **HostName** in the alarm location information. Check both the IP addresses of the management plane and service plane.
      -  **-c**: number of check times. The default value is **100**.

   -  If yes, go to :ref:`11 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134>`.
   -  If no, go to :ref:`2 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li6542838717657>`.

**Check the system environment.**

2. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li6542838717657:

   Use PuTTY to log in to the active OMS node or the node for which the alarm is generated as user **omm**.

3. Run the **cat /etc/*-release** command to check the OS type.

   -  If the OS is EulerOS, go to :ref:`4 <alm_12045__en-us_topic_0191813872_li55780683112557>`.

      .. code-block::

         # cat  /etc/*-release                                    EulerOS release 2.0 (SP2)
         EulerOS release 2.0 (SP2)

   -  If the OS is SUSE, go to :ref:`5 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li42309040172040>`.

      .. code-block::

         # cat /etc/*-release
         SUSE Linux Enterprise Server 11 (x86_64)
         VERSION = 11
         PATCHLEVEL = 3

   -  Otherwise, go to :ref:`11 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134>`.

4. .. _alm_12045__en-us_topic_0191813872_li55780683112557:

   Run the **cat /etc/euleros-release** command to check whether the OS version is EulerOS 2.2.

   .. code-block::

      # cat/etc/euleros-release
      EulerOS release 2.0 (SP2)

   -  If yes, the alarm sending function cannot be enabled. Go to :ref:`6 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li43950618195120>`.
   -  If no, go to :ref:`11 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134>`.

5. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li42309040172040:

   Run the **cat /proc/version** command to check whether the SUSE kernel version is 3.0 or later.

   .. code-block::

      # cat /proc/version
      Linux version 3.0.101-63-default (geeko@buildhost) (gcc version 4.3.4 [gcc-4_3-branch revision 152973] (SUSE Linux) ) #1 SMP Tue Jun 23 16:02:31 UTC 2015 (4b89d0c)

   -  If yes, the alarm sending function cannot be enabled. Go to :ref:`6 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li43950618195120>`.
   -  If no, go to :ref:`11 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134>`.

6. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li43950618195120:

   Log in to MRS Manager and choose **System** > **Configuration** > **Threshold Configuration**.

7.  In the navigation pane of the **Threshold Configuration** page, choose **Network Reading** > **Network Read Packet Rate Information** > **Read Packet Dropped Rate**. In the right pane, check whether **Send Alarm** is selected.

    -  If yes, the alarm sending function is enabled. Go to :ref:`8 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li38517503111027>`.
    -  If no, the alarm sending function is disabled. Go to :ref:`10 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li16613085112024>`.

8.  .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li38517503111027:

    In the right pane, deselect **Send Alarm** to shield alarm "Network Read Packet Dropped Rate Exceeds the Threshold."

9.  Go to the MRS cluster details page and choose **Alarms**.

10. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li16613085112024:

    Search for alarm 12045 and manually clear the alarms that are not automatically cleared. No further action is required.

    .. note::

       The ID of alarm Network Read Packet Dropped Rate Exceeds the Threshold is 12045.

**Check whether the NICs are bonded in active/standby mode.**

11. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134:

    Use PuTTY to log in to the node for which the alarm is generated as user **omm** and run the **ls -l /proc/net/bonding** command to check whether the **/proc/net/bonding** directory exists on the node.

    -  If yes, as shown in the following figure, the bond mode is configured for the node. Go to :ref:`12 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li56651960171744>`.

       .. code-block::

          # ls -l /proc/net/bonding/
          total 0
          -r--r--r-- 1 root root 0 Oct 11 17:35 bond0

    -  If no, the bond mode is not configured for the node. Go to :ref:`14 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li61276131112834>`.

       .. code-block::

          # ls -l /proc/net/bonding/
          ls: cannot access /proc/net/bonding/: No such file or directory

12. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li56651960171744:

    Run the **cat /proc/net/bonding/bond0** command to check whether the value of **Bonding Mode** in the configuration file is **fault-tolerance**.

    .. note::

       In the preceding command, **bond0** is the name of the bond configuration file. Use the file name obtained in :ref:`11 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4196511811134>`.

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

    -  If yes, the NICs are bonded in active/standby mode. Go to :ref:`13 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li44376005172456>`.
    -  If no, go to :ref:`14 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li61276131112834>`.

13. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li44376005172456:

    Check whether the NIC specified by **NetworkCardName** in the alarm details is the standby NIC.

    -  If yes, the alarm of the standby NIC cannot be automatically cleared. Manually clear the alarm on the alarm management page. No further action is required.
    -  If no, go to :ref:`14 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li61276131112834>`.

       .. note::

          To determine the standby NIC, check the **/proc/net/bonding/bond0** configuration file. If the NIC name corresponding to **NetworkCardName** is **Slave Interface** but not **Currently Active Slave** (the current active NIC), the NIC is the standby one.

**Check whether the threshold is set properly.**

14. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li61276131112834:

    Log in to MRS Manager and check whether the threshold (configurable, 0.5% by default) is appropriate.

    -  If yes, go to :ref:`17 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li56023883112834>`.
    -  If no, go to :ref:`15 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li47653126112834>`.

15. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li47653126112834:

    Choose **System** > **Threshold Configuration** > **Device** > **Host** > **Network Reading** > **Network Read Packet Rate Information** > **Read Packet Dropped Rate** and change the alarm threshold based on the actual service usage.

16. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`17 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li56023883112834>`.

**Check whether the network is normal.**

17. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li56023883112834:

    Contact the system administrator to check whether the network is normal.

    -  If yes, rectify the network fault and go to :ref:`18 <alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4503547112834>`.
    -  If no, go to :ref:`19 <alm_12045__en-us_topic_0191813872_li572522141314>`.

18. .. _alm_12045__en-us_topic_0191813872_en-us_topic_0087039254_li4503547112834:

    Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm_12045__en-us_topic_0191813872_li572522141314>`.

19. .. _alm_12045__en-us_topic_0191813872_li572522141314:

    Collect fault information.

    a. On MRS Manager, choose **System** > **Export Log**.
    b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
