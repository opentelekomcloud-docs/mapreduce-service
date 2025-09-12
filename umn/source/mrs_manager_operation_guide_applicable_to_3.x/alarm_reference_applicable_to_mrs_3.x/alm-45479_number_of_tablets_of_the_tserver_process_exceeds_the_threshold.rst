:original_name: ALM-45479.html

.. _ALM-45479:

ALM-45479 Number of Tablets of the Tserver Process Exceeds the Threshold
========================================================================

Alarm Description
-----------------

The system checks the Kudu service status every 60 seconds. This alarm is generated when the number of tablets of the Tserver process exceeds the threshold.

This alarm is cleared when the number of tablets of the Tserver process becomes normal and the system considers that the Kudu service recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45479    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

If the number of tablets exceeds the threshold, the query performance of the Kudu engine deteriorates.

Possible Causes
---------------

The Tserver usage is too high or the Tserver load is unbalanced.

Handling Procedure
------------------

**Handle the Kudu instance exception.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **ALM-45479 Number of Tablets of the Tserver Process Exceeds the Threshold** exists.

   -  If yes, go to :ref:`2 <alm-45479__li15820382413>`.
   -  If no, go to :ref:`6 <alm-45479__li13940112749>`.

#. .. _alm-45479__li15820382413:

   Choose **O&M** > **Alarm** > **Thresholds** > **Kudu**, locate the threshold of this alarm, compare the threshold with the monitored number of tablets in the Tserver process of the cluster, and handle the alarm accordingly.

   -  If the threshold is not properly set, change the threshold and go to :ref:`5 <alm-45479__li1282198948>`.
   -  If the Tserver load is unbalanced, go to :ref:`3 <alm-45479__li38201681243>`.
   -  If the Tserver usage is too high, delete obsolete tables or add Tserver nodes, and go to :ref:`3 <alm-45479__li38201681243>`.

#. .. _alm-45479__li38201681243:

   Log in to the Kudu node where the number of tablets exceeds the threshold.

#. Run the following commands to balance the load of the cluster (during off-peak hours, recommended):

   **su omm**

   **cd /opt/Bigdata/FusionInsight_Kudu_xxx/install/FusionInsight-Kudu-xxx/kudu/bin**

   **./kudu cluster rebalance <master_addresses> [-tables=<tables>]**

   The preceding parameters can be obtained from the KuduMaster web UI. The **tables** parameter is optional.

#. .. _alm-45479__li1282198948:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45479__li13940112749>`.

**Collect fault information.**

6. .. _alm-45479__li13940112749:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Kudu** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
