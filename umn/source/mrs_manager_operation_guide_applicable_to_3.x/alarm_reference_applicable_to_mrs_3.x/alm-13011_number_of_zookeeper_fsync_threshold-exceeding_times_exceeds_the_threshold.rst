:original_name: ALM-13011.html

.. _ALM-13011:

ALM-13011 Number of ZooKeeper fsync Threshold-Exceeding Times Exceeds the Threshold
===================================================================================

Alarm Description
-----------------

The system checks the number of times that the fsync threshold is exceeded every 30 seconds. This alarm is generated when this number exceeds the threshold for three consecutive times.

This alarm is cleared when the number of fsync threshold-exceeding times falls below the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

+-----------------------+---------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                  | Auto Cleared          |
+=======================+=================================+=======================+
| 13011                 | Critical (default threshold: 3) | Yes                   |
|                       |                                 |                       |
|                       | Major (default threshold: 2)    |                       |
+-----------------------+---------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------------+------------------------------------------------------------+
| Type                   | Parameter         | Description                                                |
+========================+===================+============================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.   |
+------------------------+-------------------+------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.   |
+------------------------+-------------------+------------------------------------------------------------+
|                        | ServiceDirectory  | Specifies the directory for which the alarm was generated. |
+------------------------+-------------------+------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.      |
+------------------------+-------------------+------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                  |
+------------------------+-------------------+------------------------------------------------------------+

Impact on the System
--------------------

ZooKeeper may fail to provide services for external systems. As a result, services of upstream components (such as Yarn, Flink, and Spark) that depend on ZooKeeper are abnormal.

Possible Causes
---------------

-  The disk storing ZooKeeper data is faulty.
-  The ZooKeeper instance encounters its processing bottleneck.
-  The threshold is improper.

Handling Procedure
------------------

**Check whether the disk is faulty.**

#. .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li60203448161840:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name for which this alarm is generated.

#. In the alarm list, check whether **ALM-12033 Slow Disk Fault** exists.

   -  If yes, go to :ref:`3 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li151971257113310>`.
   -  If no, go to :ref:`5 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li48721340111>`.

#. .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li151971257113310:

   Rectify the fault by following the handling procedure of **ALM-12033 Slow Disk Fault**.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li48721340111>`.

**Check whether the ZooKeeper instance has reached its processing bottleneck.**

5. .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li48721340111:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarms **ALM-13003 GC Duration of the ZooKeeper Process Exceeds the Threshold** and **ALM-13004 ZooKeeper Heap Memory Usage Exceeds the Threshold** exist.

   -  If yes, go to :ref:`6 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li333721612613>`.
   -  If no, go to :ref:`8 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li12794575145018>`.

6. .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li333721612613:

   Rectify the fault by following the handling procedure of **ALM-13003 GC Duration of the ZooKeeper Process Exceeds the Threshold** and **ALM-13004 ZooKeeper Heap Memory Usage Exceeds the Threshold**.

7. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li12794575145018>`.

**Check whether the threshold is customized improperly.**

8.  .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li12794575145018:

    On MRS Manager, choose **Cluster** > **Services** > **ZooKeeper** > **Instances**, click the **quorumpeer** role obtained in :ref:`1 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li60203448161840>`, and choose **Chart** > **Performance**. View the **Number of Times the ZooKeeper fsync Threshold Is Exceeded** chart and obtain the peak value within one day before and after the alarm is generated.

9.  Choose **O&M** > **Alarm** > **Thresholds**, locate the desired cluster, choose **ZooKeeper**, and click **Number of Times the ZooKeeper fsync Threshold Is Exceeded**. Click **Modify** in the **Operation** column of the **default** rule, and increase the threshold as required. Click **OK** to save the new threshold.

10. Wait 5 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li57092876161840>`.

**Collect fault information.**

11. .. _alm-13011__en-us_topic_0000002202518301_en-us_topic_0000002199610813_li57092876161840:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **ZooKeeper** for the target cluster.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
