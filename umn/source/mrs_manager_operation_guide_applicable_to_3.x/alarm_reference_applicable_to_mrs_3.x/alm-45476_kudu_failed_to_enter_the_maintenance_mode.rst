:original_name: ALM-45476.html

.. _ALM-45476:

ALM-45476 Kudu Failed to Enter the Maintenance Mode
===================================================

Alarm Description
-----------------

Kudu will enter the maintenance mode during disk replacement. This alarm is generated when Kudu fails to enter the maintenance mode.

This alarm is cleared when Kudu successfully enters the maintenance mode.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45476    Major          Yes
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
| Additional Information | Trigger Condition | Specifies the threshold for triggering the alarm.        |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

A slow or faulty disk cannot be replaced.

Possible Causes
---------------

-  The Kudu instance is abnormal, and the process cannot be stopped.
-  The permission on the **etc** configuration directory of Kudu is abnormal, and data cannot be written into the configuration file.

Handling Procedure
------------------

**Collect fault information.**

#. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
#. Expand the **Service** drop-down list, and select **Kudu** for the target cluster.
#. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.
#. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
