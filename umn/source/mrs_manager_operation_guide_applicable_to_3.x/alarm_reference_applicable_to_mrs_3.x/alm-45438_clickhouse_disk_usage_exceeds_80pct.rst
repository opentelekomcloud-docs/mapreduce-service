:original_name: ALM-45438.html

.. _ALM-45438:

ALM-45438 ClickHouse Disk Usage Exceeds 80%
===========================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the disk capacity of the ClickHouseServer node every 1 minute. This alarm is generated when the usage of the disk where the ClickHouse data directory or metadata directory resides exceeds 80%.

This alarm is automatically cleared when the usage of the disk where the ClickHouse data directory or metadata directory is located is lower than 80%.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45438    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+-------------------------------------------------------------------+
| Parameter   | Description                                                       |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| DiskPath    | Specifies the path of the disk for which the alarm is generated.  |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The ClickHouse write operation may fail.

Possible Causes
---------------

The disk capacity of the ClickHouseServer node is too small.

Handling Procedure
------------------

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.
#. Expand the disk capacity of the node for which the alarm is generated.
#. Go to :ref:`4 <alm-45438__li153021955172417>` if the expansion fails or the alarm persists after the expansion.

**Collect fault information.**

4. .. _alm-45438__li153021955172417:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

6. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
