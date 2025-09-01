:original_name: ALM-19030.html

.. _ALM-19030:

ALM-19030 P99 Latency of RegionServer RPC Request Exceeds the Threshold
=======================================================================

Alarm Description
-----------------

The system checks the P99 latency for responding to RPC requests on each RegionServer instance of the HBase service every 30 seconds. This alarm is generated when P99 latency on a RegionServer instance exceeds the threshold for 10 consecutive times.

This alarm is cleared when the P99 latency on a RegionServer instance is less than or equal to the threshold.

This alarm is generated only for MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+-------------------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                                        | Auto Cleared          |
+=======================+=======================================================+=======================+
| 19030                 | -  **Critical**: The default threshold is 10 seconds. | Yes                   |
|                       | -  **Major**: The default threshold is 5 seconds.     |                       |
+-----------------------+-------------------------------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------+----------------------------------------------------------+
| Type                   | Parameter   | Description                                              |
+========================+=============+==========================================================+
| Location Information   | Source      | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
| Additional Information | Threshold   | Specifies the threshold for generating the alarm.        |
+------------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

The RegionServer's capability of providing services for external systems is affected. For latency-sensitive services, a large number of service read and write requests may time out.

Possible Causes
---------------

-  RegionServer GC duration is too long.
-  The HDFS RPC response is too slow.
-  The client requests are at scale with high concurrency.

Handling Procedure
------------------

#. .. _alm-19030__en-us_topic_0000001821510273_li187081734191516:

   Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19030**, and view the service instance and host name in **Location**. Click the host name and record the service IP address of the host.

**Check the GC duration of the RegionServer.**

2. In the alarm list on MRS Manager, check whether the "HBase GC Duration Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19030__en-us_topic_0000001821510273_li187081734191516>`.

   -  If yes, go to :ref:`3 <alm-19030__en-us_topic_0000001821510273_li167081134161511>`.
   -  If no, go to :ref:`5 <alm-19030__en-us_topic_0000001821510273_li2708203154412>`.

3. .. _alm-19030__en-us_topic_0000001821510273_li167081134161511:

   Rectify the fault by following the handling procedure of "ALM-19007 HBase GC Duration Exceeds the Threshold".

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19030__en-us_topic_0000001821510273_li2708203154412>`.

**Check HDFS RPC response time.**

5.  .. _alm-19030__en-us_topic_0000001821510273_li2708203154412:

    In the alarm list on MRS Manager, check whether an alarm is generated for the DataNode instance of the HDFS service on which HBase depends, or whether the alarm "Slow Disk Fault", "Disk Unavailable", or "Average NameNode RPC Processing Time Exceeds the Threshold" is generated on the node where the alarm is generated.

    -  If yes, go to :ref:`6 <alm-19030__en-us_topic_0000001821510273_li87091331184413>`.
    -  If no, go to :ref:`8 <alm-19030__en-us_topic_0000001821510273_li0257150184810>`.

6.  .. _alm-19030__en-us_topic_0000001821510273_li87091331184413:

    Rectify the fault by following the handling procedure of the DataNode alarms: "ALM-12033 Slow Disk Fault", "ALM-12063 Disk Unavailable", or "ALM-14021 Average NameNode RPC Processing Time Exceeds the Threshold".

7.  Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-19030__en-us_topic_0000001821510273_li0257150184810>`.

8.  .. _alm-19030__en-us_topic_0000001821510273_li0257150184810:

    Log in to the node for which the alarm is generated, run the **iostat -x 2** command to check the disk I/O. In the command output, check whether the value in the **util** column of each disk is greater than 90%.

    -  If yes, go to :ref:`9 <alm-19030__en-us_topic_0000001821510273_li154183201810>`.
    -  If no, go to :ref:`11 <alm-19030__en-us_topic_0000001821510273_li2133184710441>`.

9.  .. _alm-19030__en-us_topic_0000001821510273_li154183201810:

    Choose **Cluster** > **Services** > **HDFS** > **Instances**, select the DataNode instance of the node for which the alarm is generated, choose **More** > **Stop Instance**, enter the password of the current user, and click **OK** to stop the DataNode instance.

10. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-19030__en-us_topic_0000001821510273_li2133184710441>`.

**Check the number of concurrent processes on a RegionServer.**

11. .. _alm-19030__en-us_topic_0000001821510273_li2133184710441:

    In the alarm list on MRS Manager, check whether the "Handler Usage of RegionServer Exceeds the Threshold" alarm is generated for the service instance in :ref:`1 <alm-19030__en-us_topic_0000001821510273_li187081734191516>`.

    -  If yes, go to :ref:`12 <alm-19030__en-us_topic_0000001821510273_li1781144374611>`.
    -  If no, go to :ref:`14 <alm-19030__en-us_topic_0000001821510273_li959275915215>`.

12. .. _alm-19030__en-us_topic_0000001821510273_li1781144374611:

    Rectify the fault by following the handling procedure of "ALM-19021 Handler Usage of RegionServer Exceeds the Threshold".

13. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-19030__en-us_topic_0000001821510273_li959275915215>`.

**Collect fault information.**

14. .. _alm-19030__en-us_topic_0000001821510273_li959275915215:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

15. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

16. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

17. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
