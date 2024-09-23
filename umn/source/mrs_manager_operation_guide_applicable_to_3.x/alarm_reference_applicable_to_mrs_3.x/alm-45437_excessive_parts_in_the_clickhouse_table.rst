:original_name: ALM-45437.html

.. _ALM-45437:

ALM-45437 Excessive Parts in the ClickHouse Table
=================================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

This alarm is generated when the number of parts exceeds the threshold specified by **part_num_threshold**.

This alarm is automatically cleared when the number of parts is less than the **part_num_threshold** value.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45437    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+------------------------------------------------------------------------------+
| Parameter   | Description                                                                  |
+=============+==============================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated.            |
+-------------+------------------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.                      |
+-------------+------------------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                         |
+-------------+------------------------------------------------------------------------------+
| Table       | Specifies the database name and table name for which the alarm is generated. |
+-------------+------------------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                         |
+-------------+------------------------------------------------------------------------------+

Impact on the System
--------------------

Service errors may occur.

Possible Causes
---------------

The data distribution in the ClickHouse table is improper, or the background merge task is executed slowly.

Handling Procedure
------------------

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  Security mode (with Kerberos enabled):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--port** 9440 **--secure**

   -  Normal mode (with Kerberos disabled):

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--user** *Username* **--password** **--port** 9000

#. Run the following command to manually merge parts:

   **optimize table** *Database name*\ **.**\ *Table name* **final;**

#. Check whether the number of parts has decreased.

   **select FQDN(), database, table, count(1) from clusterAllReplicas(default_cluster, system.parts) where database='**\ *Database name*\ **' and table='**\ *Table name*\ **' and active=1 group by (FQDN(), database, table);**

   a. If the number of parts is less than the threshold, wait for 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm-45437__li153021955172417>`.

   b. If the number of parts does not decrease, check whether the partition key of the table is set properly. If the number of partitions is too large, rectify the service logic.
   c. If the command output is empty, the table does not exist. This alarm is a historical alarm and can be ignored. Manually clear it.

**Collect fault information.**

5. .. _alm-45437__li153021955172417:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

7. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
