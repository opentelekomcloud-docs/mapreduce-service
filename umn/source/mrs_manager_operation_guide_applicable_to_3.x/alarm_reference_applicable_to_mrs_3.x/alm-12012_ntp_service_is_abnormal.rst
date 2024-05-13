:original_name: ALM-12012.html

.. _ALM-12012:

ALM-12012 NTP Service Is Abnormal
=================================

Description
-----------

The system checks whether the NTP service on a node synchronizes time with the NTP service on the active OMS node every 60 seconds. This alarm is generated when the NTP service fails to synchronize time for two consecutive times.

This alarm is generated when the time difference between the NTP service on a node and the NTP service on the active OMS node is greater than or equal to 20s for two consecutive times. This alarm is cleared when the time difference is less than 20s.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12012    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The time on the node is inconsistent with that on other nodes in the cluster. Therefore, some MRS applications on the node may not run properly.

Possible Causes
---------------

-  The NTP service on the current node cannot start properly.
-  The current node fails to synchronize time with the NTP service on the active OMS node.
-  The key value authenticated by the NTP service on the current node is inconsistent with that on the active OMS node.
-  The time offset between the node and the NTP service on the active OMS node is large.

Procedure
---------

**Check the NTP service mode of the node.**

#. .. _alm-12012__li24978126120:

   Log in to the active management node as user **root**, run the **su - omm** command to switch to user **omm**, and run the following command to check the resource status on the active and standby nodes:

   **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh**

   -  If "chrony" is displayed in the **ResName** column of the command output, go to :ref:`2 <alm-12012__li565253915220>`.
   -  If "ntp" is displayed in the **ResName** column, go to :ref:`20 <alm-12012__li18137932125120>`.

   .. note::

      If both "chrony" and "ntp" are displayed in the **ResName** column of the command output, the NTP service mode is being switched. Wait for 10 minutes and go to :ref:`1 <alm-12012__li24978126120>` again. If both "chrony" and "ntp" persist, contact O&M personnel personnel.

**Check whether the chrony service on the node is started properly.**

2. .. _alm-12012__li565253915220:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm, and view the name of the host for which the alarm is generated in **Location**.

3. Check whether the chronyd process is running on the node where the alarm is generated. Log in to the node for which the alarm is generated as user **root** and run the **ps -ef \| grep** **chronyd \| grep -v grep** command to check whether the command output contains the chronyd process.

   -  If yes, go to :ref:`6 <alm-12012__li128001354104320>`.
   -  If no, go to :ref:`4 <alm-12012__li112931223172310>`.

4. .. _alm-12012__li112931223172310:

   Run the **systemctl chronyd start** command to start the NTP service. (Currently, only CentOS and Red Hat Enterprise Linux 7.0 or later are supported.)

5. Check whether the alarm is cleared 10 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12012__li128001354104320>`.

**Check whether the current node can synchronize time properly with the chrony service on the active OMS node.**

6.  .. _alm-12012__li128001354104320:

    Check whether the node can synchronize time with the NTP service on the active OMS node based on additional information of the alarm.

    -  If yes, go to :ref:`7 <alm-12012__li920311197441>`.
    -  If no, go to :ref:`17 <alm-12012__li14800634174816>`.

7.  .. _alm-12012__li920311197441:

    Check whether the synchronization with the chrony service on the active OMS node is faulty.

    Log in to the node for which the alarm is generated as user **root** and run the **chronyc sources** command.

    In the command output, if there is an asterisk (``*``) before the IP address of the chrony service on the active OMS node, the synchronization is normal. The command output is as follows:

    .. code-block::

       MS Name/IP address         Stratum Poll Reach LastRx Last sample
       ===============================================================================
       ^* 10.10.10.162             10  10   377   626    +16us[  +15us] +/-  308us

    In the command output, if there is no asterisk (``*``) before the IP address of the NTP service on the active OMS node, and the value of **Reach** is **0**, the synchronization is abnormal.

    .. code-block::

       MS Name/IP address         Stratum Poll Reach LastRx Last sample
       ===============================================================================
       ^? 10.1.1.1                      0  10     0     -     +0ns[   +0ns] +/-    0ns

    -  If yes, go to :ref:`8 <alm-12012__li10140131164518>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

8.  .. _alm-12012__li10140131164518:

    The chrony synchronization failure is typically caused by the system firewall. If the firewall can be disabled, disable it. If the firewall cannot be disabled, check the firewall configuration policy and ensure that UDP ports 123 and 323 are not disabled. (For details, see the firewall configuration policy of each system.)

9.  Check whether the alarm is cleared 10 minutes later.

    -  If yes, no further action is required.
    -  If no, go to :ref:`10 <alm-12012__li876311455457>`.

10. .. _alm-12012__li876311455457:

    Log in to the active OMS node as user **root** and run the following command to view the authentication code whose key value index is **1M**:

    In Red Hat Enterprise Linux, run the **cat ${BIGDATA_HOME}/om-server/OMS/workspace/conf/chrony.keys** command.

11. Run the following command to check whether the key value is the same as that queried in :ref:`10 <alm-12012__li876311455457>`:

    In Red Hat Enterprise Linux, run the **diff ${BIGDATA_HOME}/om-server/OMS/workspace/conf/chrony.keys /etc/chrony.keys** command.

    .. note::

       If the key values are the same, no result is returned after the command is executed. For example:

       .. code-block::

          host01:~ # cat ${BIGDATA_HOME}/om-server/OMS/workspace/conf/chrony.keys
          1 M sdYbq;o^CzEAWo<U=Tw5
          host01:~ # diff ${BIGDATA_HOME}/om-server/OMS/workspace/conf/chrony.keys /etc/chrony.keys
          host01:~ #

    -  If yes, go to :ref:`12 <alm-12012__li126135154610>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

12. .. _alm-12012__li126135154610:

    Run the **cat ${BIGDATA_HOME}/om-server/om/packaged-distributables/ntpKeyFile** command to check whether the key value is the same as that queried in :ref:`10 <alm-12012__li876311455457>`. (Compare the key value with that of the authentication key index field **1M** queried in :ref:`10 <alm-12012__li876311455457>`.)

    -  If yes, go to :ref:`13 <alm-12012__li119741549194615>`.
    -  If no, go to :ref:`15 <alm-12012__li12237374714>`.

13. .. _alm-12012__li119741549194615:

    Log in to the faulty node as user **root** and run the **cat /etc/chrony.keys** command in Red Hat Enterprise Linux to check whether the key value is the same as the value queried in :ref:`12 <alm-12012__li126135154610>` (use the key value of the authentication key index field **1M** for comparison).

    -  If yes, go to :ref:`38 <alm-12012__li3559109817193>`.
    -  If no, go to :ref:`14 <alm-12012__li1811911136195>`.

14. .. _alm-12012__li1811911136195:

    Run the **su - omm** command to switch to user **omm**, change the key value of the authentication key index field **1M** in **${NODE_AGENT_HOME}/chrony.keys** to the key value of **ntpKeyFile** in :ref:`12 <alm-12012__li126135154610>`, and go to :ref:`16 <alm-12012__li1681623204717>`.

15. .. _alm-12012__li12237374714:

    Run the following commands as user **root** or **omm** to change the NTP key value of the active OMS node (change **ntp.keys** to **ntpkeys** in Red Hat Enterprise Linux):

    **cd ${BIGDATA_HOME}/om-server/OMS/workspace/conf**

    **sed -i "`cat chrony.keys \| grep -n '1 M'|awk -F ':' '{print $1}'`d" chrony.keys**

    **echo "1 M \`cat ${BIGDATA_HOME}/om-server/om/packaged-distributables/ntpKeyFile`" >> chrony.keys**

    Check whether the key value of the authentication key index field **1M** in **chrony.keys** is the same as that of **ntpKeyFile**.

    -  If yes, go to :ref:`16 <alm-12012__li1681623204717>`.
    -  If no, change the key value of the authentication key index field **1M** in **chrony.keys** to the key value of **ntpKeyFile** and go to :ref:`16 <alm-12012__li1681623204717>`.

16. .. _alm-12012__li1681623204717:

    After 5 minutes, run the **systemctl chronyd restart** command to restart the chrony service on the active OMS node. After 15 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

**Check whether the time deviation between the node and the chrony service on the active OMS node is large.**

17. .. _alm-12012__li14800634174816:

    Check whether the time deviation is large in additional information of the alarm.

    -  If yes, go to :ref:`18 <alm-12012__li72571946124812>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

18. .. _alm-12012__li72571946124812:

    On the **Hosts** tab page, select the host for which the alarm is generated, and choose **More** > **Stop All Instances** to stop all the services on the node.

    If the time on the alarm node is later than that on the chrony service of the active OMS node, adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Instances** to start the services on the node.

    If the time on the alarm node is earlier than that on the chrony service of the active OMS node, wait until the time deviation is due and adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Instances** to start the services on the node.

    .. note::

       If you do not wait, data loss may occur.

19. After 10 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

**Check whether the NTP service on the node is started properly.**

20. .. _alm-12012__li18137932125120:

    On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image2| in the row containing the alarm, and view the name of the host for which the alarm is generated in **Location**.

21. Check whether the ntpd process is running on the node using the following method. Log in to the alarm node as user **root** and run the **ps -ef \| grep ntpd \| grep -v grep** command to check whether the command output contains the ntpd process.

    -  If yes, go to :ref:`24 <alm-12012__li3507541817193>`.
    -  If no, go to :ref:`22 <alm-12012__li797292017193>`.

22. .. _alm-12012__li797292017193:

    Run the **service ntp start** command (or the **service ntpd start** command in Red Hat Enterprise Linux) to start the NTP service.

23. After 10 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`24 <alm-12012__li3507541817193>`.

**Check whether the node can synchronize time properly with the NTP service on the active OMS node.**

24. .. _alm-12012__li3507541817193:

    Check whether the node can synchronize time with the NTP service on the active OMS node based on additional information of the alarm.

    -  If yes, go to :ref:`25 <alm-12012__li3019831317193>`.
    -  If no, go to :ref:`35 <alm-12012__li766317817193>`.

25. .. _alm-12012__li3019831317193:

    Check whether the synchronization with the NTP service on the active OMS node is faulty.

    Log in to the alarm node as user **root** and run the **ntpq -np** command.

    If an asterisk (``*``) exists before the IP address of the NTP service on the active OMS node in the command output, the synchronization is in normal state. The command output is as follows:

    .. code-block::

       remote refid st t when poll reach delay offset jitter
       ==============================================================================
       *10.10.10.162 .LOCL. 1 u 1 16 377 0.270 -1.562 0.014

    If there is no asterisk (``*``) before the IP address of the NTP service on the active OMS node, as shown in the following command output, and the value of **refid** is **.INIT.**, the synchronization is abnormal.

    .. code-block::

       remote refid st t when poll reach delay offset jitter
       ==============================================================================
       10.10.10.162 .INIT. 1 u 1 16 377 0.270 -1.562 0.014

    -  If yes, go to :ref:`26 <alm-12012__li14622157181719>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

26. .. _alm-12012__li14622157181719:

    The NTP synchronization failure is typically caused by the system firewall. If the firewall can be disabled, run the **iptables -F** command to disable it. If the firewall cannot be disabled, run the **iptables -L** command to check the firewall configuration policy and ensure that the UDP port 123 is not disabled. (For details, see the firewall configuration policy of each system.)

27. After 10 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`28 <alm-12012__li50636830155013>`.

28. .. _alm-12012__li50636830155013:

    Log in to the active OMS node as user **root** and run the following command to view the authentication key index field **1M**:

    In SUSE Linux, run the **cat ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntp.keys** command.

    In Red Hat Enterprise Linux or EulerOS, run the **cat ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntpkeys** command.

29. Run the following command to check whether the key value is the same as that queried in :ref:`28 <alm-12012__li50636830155013>`:

    In SUSE Linux, run the **diff ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntp.keys /etc/ntp.keys** command.

    In Red Hat Enterprise Linux or EulerOS, run the **diff ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntpkeys /etc/ntp/ntpkeys** command.

    .. note::

       If the key values are the same, no result is returned after the command is executed. For example:

       .. code-block::

          host01:~ # cat ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntp.keys
          1 M sdYbq;o^CzEAWo<U=Tw5
          host01:~ # diff ${BIGDATA_HOME}/om-server/OMS/workspace/conf/ntp.keys /etc/ntp.keys
          host01:~ #

    -  If yes, go to :ref:`30 <alm-12012__li58889465155013>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

30. .. _alm-12012__li58889465155013:

    Run the **cat ${BIGDATA_HOME}/om-server/om/packaged-distributables/ntpKeyFile** command to check whether the key value is the same as that queried in :ref:`28 <alm-12012__li50636830155013>`. (Compare the key value with that of the authentication key index field **1M** queried in :ref:`28 <alm-12012__li50636830155013>`.)

    -  If yes, go to :ref:`31 <alm-12012__li44851587155013>`.
    -  If no, go to :ref:`33 <alm-12012__li22747884155013>`.

31. .. _alm-12012__li44851587155013:

    Log in to the faulty node as user **root** and run the **cat /etc/ntp.keys** command in SUSE Linux (or the **cat /etc/ntp/ntpkeys** command in Red Hat Enterprise Linux) to check whether the key value is the same as the value queried in :ref:`30 <alm-12012__li58889465155013>` (use the key value of the authentication key index field **1M** for comparison).

    -  If yes, go to :ref:`38 <alm-12012__li3559109817193>`.
    -  If no, go to :ref:`32 <alm-12012__li817715392262>`.

32. .. _alm-12012__li817715392262:

    Run the **su - omm** command to switch to user **omm**, change the key value of the authentication key index field **1M** in **${NODE_AGENT_HOME}/ntp.keys** (**${NODE_AGENT_HOME}/ntpkeys** in Red Hat Enterprise Linux) to the key value of **ntpKeyFile** in :ref:`30 <alm-12012__li58889465155013>`, and go to :ref:`34 <alm-12012__li30141735155013>`.

33. .. _alm-12012__li22747884155013:

    Run the following commands as user **root** or **omm** to change the NTP key value of the active OMS node (change **ntp.keys** to **ntpkeys** in Red Hat Enterprise Linux):

    **cd ${BIGDATA_HOME}/om-server/OMS/workspace/conf**

    **sed -i "`cat ntp.keys \| grep -n '1 M'|awk -F ':' '{print $1}'`d" ntp.keys**

    **echo "1 M \`cat ${BIGDATA_HOME}/om-server/om/packaged-distributables/ntpKeyFile`" >>ntp.keys**

    Check whether the key value of the authentication key index field **1M** in **ntp.keys** is the same as that of **ntpKeyFile**.

    -  If yes, go to :ref:`34 <alm-12012__li30141735155013>`.
    -  If no, change the key value of the authentication key index field **1M** in **ntp.keys** to the key value of **ntpKeyFile** and go to :ref:`34 <alm-12012__li30141735155013>`.

34. .. _alm-12012__li30141735155013:

    After 5 minutes, run the **service ntp restart** command to restart the NTP service on the active OMS node. After 15 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

**Check whether the time deviation between the node and the NTP service on the active OMS node is large.**

35. .. _alm-12012__li766317817193:

    Check whether the time deviation is large in additional information of the alarm.

    -  If yes, go to :ref:`36 <alm-12012__li5505704717193>`.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

36. .. _alm-12012__li5505704717193:

    On the **Hosts** tab page, select the host for which the alarm is generated, and choose **More** > **Stop All Instances** to stop all the services on the node.

    If the time on the alarm node is later than that on the NTP service of the active OMS node, adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Instances** to start the services on the node.

    If the time on the alarm node is earlier than that on the NTP service of the active OMS node, wait until the time deviation is due and adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Instances** to start the services on the node.

    .. note::

       If you do not wait, data loss may occur.

37. After 10 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`38 <alm-12012__li3559109817193>`.

**Collect the fault information.**

38. .. _alm-12012__li3559109817193:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

39. In the **Services** area, select **NodeAgent** and **OmmServer**, and click **OK**. Expand the **Hosts** dialog box and select the alarm node and the active OMS node.

40. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

41. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087389.png
.. |image2| image:: /_static/images/en-us_image_0000001532448250.png
.. |image3| image:: /_static/images/en-us_image_0000001532767474.png
