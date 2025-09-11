:original_name: ALM-45475.html

.. _ALM-45475:

ALM-45475 A Single Replica Exists in the Kudu Data Table
========================================================

Alarm Description
-----------------

The system checks the replica status of the Kudu data table. This alarm is generated when a single replica is detected in the Kudu data table.

This alarm is cleared when all Kudu data tables have multiple replicas or no data.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45475    Major          Yes
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

If a hardware fault occurs, for example, a slow disk or a faulty disk, the Kudu data table may lose data.

Handling Procedure
------------------

#. Run the following command to query details about each data table and check for the table with only one replica:

   **kudu table describe** *{Kudu master address (separated by commas)}* *{Data table name}*

   You can view details about the table with only one replica on the Kudu web UI.

**Collect fault information.**

2. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
3. Expand the **Service** drop-down list, and select **Kudu** for the target cluster.
4. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.
5. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
