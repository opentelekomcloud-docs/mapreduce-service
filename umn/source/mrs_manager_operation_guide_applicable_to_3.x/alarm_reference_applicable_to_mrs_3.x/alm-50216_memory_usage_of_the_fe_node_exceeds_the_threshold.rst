:original_name: ALM-50216.html

.. _ALM-50216:

ALM-50216 Memory Usage of the FE Node Exceeds the Threshold
===========================================================

Alarm Description
-----------------

The system checks the memory usage of the FE node every 30 seconds. This alarm is generated when the memory usage exceeds the threshold (95% by default).

This alarm is cleared when the memory usage of the FE node falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50216    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+-------------------------------------------------------------------+
| Parameter         | Description                                                       |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Task execution and client connection to the FE are affected.

Possible Causes
---------------

The FE heap memory is too small.

Handling Procedure
------------------

**Check the FE heap memory usage.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds**, select the name of the desired cluster, and choose **Doris** > **CPU and Memory** > **Memory usage of the FE node (FE)**.

   a. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.
   b. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.

#. Log in to the FE node for which the alarm is generated as user **omm**, run the **top** command to check the memory usage of processes, locate the process with high memory usage, and check whether the process belongs to the current service and is running properly.

   -  If yes, go to :ref:`3 <alm-50216__li39538131277>`.
   -  If no, isolate or stop the process, or adjust the memory size, and check whether the memory is released.

#. .. _alm-50216__li39538131277:

   Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-50216__li29521913475>`.

   .. important::

      -  During the restart of the Doris service, the Doris service is unavailable and cannot provide services for external systems. Tasks connected to the Doris service fail.
      -  During instance restart, the tasks running on the nodes of the instance will fail. The tasks on instance nodes that are not restarted are not affected.

**Collect fault information.**

4. .. _alm-50216__li29521913475:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **Doris** for the target cluster.

6. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
