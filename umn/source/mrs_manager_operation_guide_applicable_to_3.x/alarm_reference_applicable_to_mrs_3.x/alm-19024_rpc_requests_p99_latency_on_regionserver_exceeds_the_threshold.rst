:original_name: ALM-19024.html

.. _ALM-19024:

ALM-19024 RPC Requests P99 Latency on RegionServer Exceeds the Threshold
========================================================================

Alarm Description
-----------------

The system checks P99 latency for RPC requests on each RegionServer instance of the HBase service every 30 seconds. This alarm is generated when P99 latency for RPC requests on a RegionServer exceeds the threshold for 10 consecutive times.

This alarm is cleared when P99 latency for RPC requests on a RegionServer instance is less than or equal to the threshold.

This alarm applies only to MRS 3.3.0 or later.

Alarm Attributes
----------------

+-----------------------+-------------------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                                        | Auto Cleared          |
+=======================+=======================================================+=======================+
| 19024                 | -  **Critical**: The default threshold is 10 seconds. | Yes                   |
|                       | -  **Major**: The default threshold is 5 seconds.     |                       |
+-----------------------+-------------------------------------------------------+-----------------------+

Alarm Parameters
----------------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

If RPC requests P99 latency exceeds the threshold, the RegionServer cannot deliver normal service performance externally. If RPC requests P99 latency on most RegionServers in the cluster exceeds the threshold, HBase may fail to provide services for external systems.

Possible Causes
---------------

-  RegionServer GC duration is too long.
-  The HDFS RPC response is too slow.
-  RegionServer request concurrency is too high.

Handling Procedure
------------------

#. .. _alm-19024__li187081734191516:

   Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19024**, and view the service instance and host name in **Location**.

**Check the GC duration of RegionServer.**

2. In the alarm list on FusionInsight Manager, check whether the "HBase GC Duration Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19024__li187081734191516>`.

   -  If yes, go to :ref:`3 <alm-19024__li167081134161511>`.
   -  If no, go to :ref:`5 <alm-19024__li2708203154412>`.

3. .. _alm-19024__li167081134161511:

   Rectify the fault by following the handling procedure of "ALM-19007 HBase GC Duration Exceeds the Threshold".

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19024__li2708203154412>`.

**Check HDFS RPC response time.**

5. .. _alm-19024__li2708203154412:

   In the alarm list on FusionInsight Manager, check whether alarm "Average NameNode RPC Processing Time Exceeds the Threshold" is generated for the HDFS service on which the HBase service depends.

   -  If yes, go to :ref:`6 <alm-19024__li87091331184413>`.
   -  If no, go to :ref:`8 <alm-19024__li2133184710441>`.

6. .. _alm-19024__li87091331184413:

   Rectify the fault by following the handling procedure of "ALM-14021 Average NameNode RPC Processing Time Exceeds the Threshold".

7. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-19024__li2133184710441>`.

**Check the number of concurrent processes on a RegionServer.**

8.  .. _alm-19024__li2133184710441:

    In the alarm list on FusionInsight Manager, check whether the "Handler Usage of RegionServer Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19024__li187081734191516>`.

    -  If yes, go to :ref:`9 <alm-19024__li1781144374611>`.
    -  If no, go to :ref:`11 <alm-19024__li959275915215>`.

9.  .. _alm-19024__li1781144374611:

    Rectify the fault by following the handling procedure of "ALM-19021 Handler Usage of RegionServer Exceeds the Threshold".

10. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-19024__li959275915215>`.

**Collect fault information.**

11. .. _alm-19024__li959275915215:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
