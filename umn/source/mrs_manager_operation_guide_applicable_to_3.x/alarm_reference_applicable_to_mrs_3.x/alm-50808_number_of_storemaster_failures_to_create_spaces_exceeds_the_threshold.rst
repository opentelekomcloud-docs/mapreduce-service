:original_name: ALM-50808.html

.. _ALM-50808:

ALM-50808 Number of StoreMaster Failures to Create Spaces Exceeds the Threshold
===============================================================================

Alarm Description
-----------------

The system checks whether StoreMaster fails to create a space every 30 seconds. This alarm is generated when StoreMaster fails to create a space.

This alarm is cleared when no space fails to be created.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50808    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The corresponding Spark task fails.

Possible Causes
---------------

Access to ZooKeeper is abnormal.

Handling Procedure
------------------

**Check the ZooKeeper instance status.**

#. On MRS Manager, choose **Cluster** > **Services** > **ZooKeeper** > **Instances**.

#. Check whether ZooKeeper instances are normal.

   -  If yes, go to :ref:`6 <alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li13391111735>`.
   -  If no, go to :ref:`3 <alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li23391411432>`.

#. .. _alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li23391411432:

   Select the instances whose status is not **Normal**, click **More**, and select **Restart Instance**.

#. Check whether the instance status becomes normal after the restart.

   -  If yes, go to :ref:`5 <alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li4339816317>`.
   -  If no, go to :ref:`6 <alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li13391111735>`.

#. .. _alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li4339816317:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li13391111735>`.

**Collect fault information.**

6. .. _alm-50808__en-us_topic_0000002520347221_en-us_topic_0000002192665153_li13391111735:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
