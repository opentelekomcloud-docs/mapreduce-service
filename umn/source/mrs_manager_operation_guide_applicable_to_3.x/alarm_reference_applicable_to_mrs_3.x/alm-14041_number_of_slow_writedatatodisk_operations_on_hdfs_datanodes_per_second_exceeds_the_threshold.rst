:original_name: ALM-14041.html

.. _ALM-14041:

ALM-14041 Number of Slow WriteDataToDisk Operations on HDFS DataNodes per Second Exceeds the Threshold
======================================================================================================

Alarm Description
-----------------

The system checks the number of slow WriteDataToDisk operations per second of HDFS DataNode instances every 60 seconds and compares the number with the threshold. This alarm is generated when this number has exceeded the threshold for three minutes.

This alarm is cleared when the number of slow WriteDataToDisk operations per second of the HDFS DataNode instance is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
14041    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Slow WriteDataToDisk operations on HDFS affect the data read and write performance of HDFS.

Possible Causes
---------------

-  The alarm threshold is improperly set.
-  The disk I/O rate of the HDFS DataNode instance is low, and the HDFS DataNode processing capability reaches the bottleneck.

Handling Procedure
------------------

**Check whether the alarm threshold is set properly.**

#. .. _alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li23652015192818:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name of the DataNode instance for which this alarm is generated.

#. Choose **Cluster** > **Services** > **HDFS**, click the **Instances** tab, and click the DataNode role based on the host name obtained in :ref:`1 <alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li23652015192818>`.

#. Choose **Chart** > **Performance**, view the **Slow Write Data To Disk Count Per Second** chart, and obtain the peak value within one day before and after the alarm is generated.

#. Choose **O&M** > **Alarm** > **Thresholds**, locate the desired cluster, choose **HDFS**, and click **Slow Write Data To Disk Count Per Second**. Click **Modify** in the **Operation** column of the **default** rule, and change the threshold to 150% of the peak value displayed within one day before and after the alarm is generated. Click **OK** to save the new threshold.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li10137515202318>`.

**Check whether the disk is faulty.**

6. .. _alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li10137515202318:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms** and check whether **ALM-12033 Slow Disk Fault** exists.

   -  If yes, go to :ref:`7 <alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li11371715202313>`.
   -  If no, go to :ref:`9 <alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li42224042151734>`.

7. .. _alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li11371715202313:

   Rectify the fault by following the handling procedure of **ALM-12033 Slow Disk Fault**.

8. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li42224042151734>`.

**Collect fault information.**

9.  .. _alm-14041__en-us_topic_0000002201350941_en-us_topic_0000002186812789_li42224042151734:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **HDFS** for the target cluster.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
