:original_name: ALM-50818.html

.. _ALM-50818:

ALM-50818 Percentage of StoreWorker SDK Network Connections to the Configured Upper Limit Exceeds the Threshold
===============================================================================================================

Alarm Description
-----------------

The system checks the percentage of StoreWorker SDK network connections to the upper limit every 30 seconds. This alarm is generated when the percentage exceeds the threshold.

This alarm is cleared when the percentage of StoreWorker SDK network connections to the upper limit falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50818    Major          Yes
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

If the number of connections is too large, the memory usage increases. As a result, the service processing efficiency decreases and tasks may fail.

Possible Causes
---------------

-  The load tilt is too large, and the load pressure is too high.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **Resources** > **Percentage of StoreWorker SDK network connections to the configured upper limit (StoreWorker)**.
#. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

#. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.
#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50818__en-us_topic_0000002520347225_en-us_topic_0000002192665161_li10360155511379>`.

**Collect fault information.**

5. .. _alm-50818__en-us_topic_0000002520347225_en-us_topic_0000002192665161_li10360155511379:

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
