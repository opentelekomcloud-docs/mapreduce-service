:original_name: ALM-50820.html

.. _ALM-50820:

ALM-50820 Memory Usage of the StoreWorker Process Exceeds the Threshold
=======================================================================

Alarm Description
-----------------

The system checks the StoreWorker memory usage every 30 seconds. This alarm is generated when the memory usage exceeds the threshold.

This alarm is cleared when the StoreWorker memory usage falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50820    Major          Yes
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

If the memory usage exceeds the Cgroup limit, the processes will be terminated by Cgroups.

Possible Causes
---------------

-  The load pressure is too high.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **MEMORY** > **Memory usage of the worker process (StoreWorker)**.
#. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

#. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.
#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50820__en-us_topic_0000002488107400_en-us_topic_0000002192819525_li10360155511379>`.

**Collect fault information.**

5. .. _alm-50820__en-us_topic_0000002488107400_en-us_topic_0000002192819525_li10360155511379:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
