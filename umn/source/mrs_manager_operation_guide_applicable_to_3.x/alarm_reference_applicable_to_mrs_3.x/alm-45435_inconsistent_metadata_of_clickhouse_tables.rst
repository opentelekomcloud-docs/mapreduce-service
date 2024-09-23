:original_name: ALM-45435.html

.. _ALM-45435:

ALM-45435 Inconsistent Metadata of ClickHouse Tables
====================================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

This alarm is generated when the metadata in a distributed table or in the local table of the distributed table has been inconsistent for 180 min.

This alarm is automatically cleared when the metadata in the distributed table or in the local table of the distributed table becomes consistent.

Metadata consistency includes:

-  Consistent quantity, name, sequence, and type of each column in the table
-  Consistent partition keys
-  Consistent sorting keys
-  Consistent primary keys
-  Consistent sampling keys

.. note::

   If this alarm exists, table metadata is inconsistent in the ClickHouse cluster to which the current node belongs. The inconsistency may be caused by multiple reasons, not limited to those mentioned in additional information.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45435    Minor          Yes
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

Subsequent operations such as INSERT and ALTER on the table may fail.

Possible Causes
---------------

Table metadata modification fails or is not executed on one or more ClickHouseServer nodes.

Handling Procedure
------------------

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--user** *Username* **--password** **--port** 9000

#. Check whether any task is being executed for the table to which the alarm is generated.

   Run the following command to check whether any SQL task is being executed:

   **select \* from system.processes where current_database='**\ *Database name*\ **' and query like '%**\ *Table name*\ **%'**

   Run the following command to check whether a mutation task is being executed:

   **select \* from system.mutations where database=**\ *'Database name'* **and table=**\ *'Table name'*\ **;**

   -  If the query result is empty, go to :ref:`4 <alm-45435__li2088812501189>`.

   -  If the query result contains error information, rectify the fault accordingly. If the fault cannot be rectified based on the error information, go to :ref:`6 <alm-45435__li153021955172417>`.

   -  If the query result contains information about an on-going task with no error, the SQL/mutation task is being executed.

      Wait for 5 minutes. If the alarm is cleared, no further action is required. If the alarm persists, go to :ref:`4 <alm-45435__li2088812501189>`.

#. .. _alm-45435__li2088812501189:

   Modify the table structure, delete a table, or add a table based on service requirements until the table metadata of all nodes in the cluster is consistent. After 5 minutes, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45435__li1346013391892>`.

5. .. _alm-45435__li1346013391892:

   If the table has been deleted, manually clear the alarm and check whether the alarm is reported again.

   -  If yes, go to :ref:`6 <alm-45435__li153021955172417>`.
   -  If no, no further action is required.

**Collect fault information.**

6.  .. _alm-45435__li153021955172417:

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
