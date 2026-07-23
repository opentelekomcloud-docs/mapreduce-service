:original_name: ALM-50828.html

.. _ALM-50828:

ALM-50828 StoreWorker Data Loss Errors Exceed the Threshold
===========================================================

Alarm Description
-----------------

The system checks StoreWorker data loss errors every 30 seconds. This alarm is generated when the number of data loss errors exceeds the threshold.

This alarm is cleared when the number of data loss errors falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50828    Major          Yes
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

If data is lost, data recalculation is triggered, and tasks in the entire phase need to be re-executed. Recalculation consumes a large number of resources and has a significant impact on performance.

Possible Causes
---------------

-  Two or more nodes are faulty.
-  Data is tampered with.

Handling Procedure
------------------

**Check the MemArtsStore instance status.**

#. On MRS Manager, choose **Cluster** > **Services** > **MemArtsStore** > **Instances**.

#. Check whether MemArtsStore instances are normal.

   -  If yes, go to :ref:`6 <alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li10360155511379>`.
   -  If no, go to :ref:`3 <alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li105001846177>`.

#. .. _alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li105001846177:

   Select the instances whose status is not **Normal**, click **More**, and select **Restart Instance**.

#. Check whether the instance status becomes normal after the restart.

   -  If yes, go to :ref:`5 <alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li150034614718>`.
   -  If no, go to :ref:`6 <alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li10360155511379>`.

#. .. _alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li150034614718:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li10360155511379>`.

**Collect fault information.**

6. .. _alm-50828__en-us_topic_0000002488107404_en-us_topic_0000002192819533_li10360155511379:

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
