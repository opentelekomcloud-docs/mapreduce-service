:original_name: ALM-45436.html

.. _ALM-45436:

ALM-45436 Skew ClickHouse Table Data
====================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

This alarm is generated when data skew occurs in the local table of a distributed table between ClickHouse nodes. This alarm is automatically cleared when data becomes balanced.

Data skew check method:

-  If **min_table_check_data_bytes** is set to **0**, data skew check is disabled.
-  If **min_table_check_data_bytes** is greater than **0**, data skew check is enabled.

After data skew check is enabled, if the data volume in a table is less than the **min_table_check_data_bytes** value, no alarm will be reported due to data skew. When the data volume is greater than the **min_table_check_data_bytes** value and the data volume difference between the same table on different nodes is greater than the percentage specified in **min_table_data_varies_rate**, data skew occurs and this alarm is reported.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45436    Minor          Yes
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

Impact on the System
--------------------

SQL execution efficiency may be lowered.

Possible Causes
---------------

The data write policy is improper, causing unbalanced data among nodes.

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

#. View data distribution.

   **select FQDN(), database, table, sum(data_compressed_bytes) from clusterAllReplicas(**\ *Name of the logical cluster*\ **, system.parts) where database='**\ *Database name*\ **' and table='**\ *Table name*\ **' and active=1 group by (FQDN(), database, table);**

#. Balance data with a few clicks or migrate data based on service requirements.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45436__li153021955172417>`.

**Collect fault information.**

6.  .. _alm-45436__li153021955172417:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

8.  Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
