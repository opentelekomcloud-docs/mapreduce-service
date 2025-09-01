:original_name: ALM-19034.html

.. _ALM-19034:

ALM-19034 Number of RegionServer WAL Write Timeouts Exceeds the Threshold
=========================================================================

Alarm Description
-----------------

The system checks the number of RegionServer WAL write timeouts in each HBase service every 30 seconds. This alarm is generated when the number of WAL write timeouts on a RegionServer instance exceeds the threshold for 10 consecutive times.

This alarm is cleared when the number of WAL write timeouts on a RegionServer instance is less than or equal to the threshold.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+--------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                       | Auto Cleared          |
+=======================+======================================+=======================+
| 19034                 | -  Critical (default threshold: 500) | Yes                   |
|                       | -  Major (default threshold: 300)    |                       |
+-----------------------+--------------------------------------+-----------------------+

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

The write operation latency increases. Too many WAL write timeouts may severely deteriorate the data write performance.

Possible Causes
---------------

-  A slow disk fault occurred.
-  RegionServer GC is abnormal.
-  HBase is overloaded.
-  The WAL configuration is improper.

Handling Procedure
------------------

#. .. _alm-19034__en-us_topic_0000001821510277_li187081734191516:

   Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19034**, and view the service instance and host name in **Location**.

**Check whether a slow disk fault occurred.**

2. In the alarm list on MRS Manager, check whether the "Slow Disk Fault" or "Disk Unavailable" is displayed for the instance you checked in :ref:`1 <alm-19034__en-us_topic_0000001821510277_li187081734191516>`.

   -  If yes, go to :ref:`3 <alm-19034__en-us_topic_0000001821510277_li167081134161511>`.
   -  If no, go to :ref:`5 <alm-19034__en-us_topic_0000001821510277_li37535318412>`.

3. .. _alm-19034__en-us_topic_0000001821510277_li167081134161511:

   Rectify the fault by following the handling procedure of "ALM-12033 Slow Disk Fault" or "ALM-12063 Disk Unavailable".

4. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19034__en-us_topic_0000001821510277_li37535318412>`.

**Check whether RegionServer GC is abnormal.**

5. .. _alm-19034__en-us_topic_0000001821510277_li37535318412:

   In the alarm list on MRS Manager, check whether "ALM-19007 HBase GC Duration Exceeds the Threshold" is displayed.

   -  If yes, go to :ref:`6 <alm-19034__en-us_topic_0000001821510277_li666128618>`.
   -  If no, go to :ref:`8 <alm-19034__en-us_topic_0000001821510277_li2708203154412>`.

6. .. _alm-19034__en-us_topic_0000001821510277_li666128618:

   Rectify the fault by following the handling procedure of "ALM-19007 HBase GC Duration Exceeds the Threshold".

7. Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-19034__en-us_topic_0000001821510277_li2708203154412>`.

**Check the HBase load.**

8.  .. _alm-19034__en-us_topic_0000001821510277_li2708203154412:

    In the alarm list on MRS Manager, check whether "ALM-19018 HBase Compaction Queue Size Exceeds the Threshold" is displayed.

    -  If yes, go to :ref:`9 <alm-19034__en-us_topic_0000001821510277_li431018531018>`.
    -  If no, go to :ref:`11 <alm-19034__en-us_topic_0000001821510277_li1435343019397>`.

9.  .. _alm-19034__en-us_topic_0000001821510277_li431018531018:

    Rectify the fault by following the handling procedure of "ALM-19018 HBase Compaction Queue Size Exceeds the Threshold".

10. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-19034__en-us_topic_0000001821510277_li1435343019397>`.

**Check the WAL configuration.**

11. .. _alm-19034__en-us_topic_0000001821510277_li1435343019397:

    On MRS Manager, choose **Cluster** > **Service** > **HBase**, click **Configurations** > **All Configurations**, and check whether the values of **hbase.wal.hsync** and **hbase.hfile.hsync** are **true**.

    -  If yes, go to :ref:`12 <alm-19034__en-us_topic_0000001821510277_li12678144164214>`.
    -  If no, go to :ref:`14 <alm-19034__en-us_topic_0000001821510277_li959275915215>`.

12. .. _alm-19034__en-us_topic_0000001821510277_li12678144164214:

    Set both **hbase.wal.hsync** and **hbase.hfile.hsync** to **false** and click **Save**. Click **Dashboard** and click **More** > **Restart Service** to restart the HBase service.

    .. important::

       During HBase service restart, the service is unavailable. For example, data cannot be read or written, table operations cannot be performed, and the HBase web UI is inaccessible.

13. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-19034__en-us_topic_0000001821510277_li959275915215>`.

**Collect fault information.**

14. .. _alm-19034__en-us_topic_0000001821510277_li959275915215:

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
