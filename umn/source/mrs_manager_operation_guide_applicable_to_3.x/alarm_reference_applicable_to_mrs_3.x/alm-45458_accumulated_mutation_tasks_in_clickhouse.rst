:original_name: ALM-45458.html

.. _ALM-45458:

ALM-45458 Accumulated Mutation Tasks in ClickHouse
==================================================

.. note::

   This section applies only to MRS 3.6.0-LTS or later.

Alarm Description
-----------------

The alarm module checks the number of tasks in the mutations queue of the ClickHouse service every 30 seconds. This alarm is generated when the alarm module detects that the number exceeds the threshold (5,000).

This alarm is cleared when the number of tasks falls below the threshold.

Alarm Attributes
----------------

+-----------------------+---------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                              | Auto Cleared          |
+=======================+=============================================+=======================+
| 45458                 | Critical (The default threshold is 10,000.) | Yes                   |
|                       |                                             |                       |
|                       | Major (The default threshold is 5,000.)     |                       |
+-----------------------+---------------------------------------------+-----------------------+

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

When mutation tasks are stacked on the ClickHouse node, task query may be delayed. In severe cases, the performance of the entire cluster is affected, and even the cluster service becomes unavailable.

Possible Causes
---------------

-  ALTER TABLE ... UPDATE/DELETE tasks are frequently executed.
-  The table contains dirty data. As a result, the mutation tasks fail to be executed and are retried repeatedly.

Handling Procedure
------------------

**Check whether there are ALTER TABLE ... UPDATE/DELETE tasks being frequently executed.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user**\ *Username* **--password --port** 9440

#. .. _alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li14242152404310:

   Run the following statement to check the task type in **system.mutations** and check whether there is a mutation task that has not been executed for a long time (more than 10 minutes):

   .. code-block::

      select FQDN() as node, database, table, mutation_id, create_time, command, is_done, parts_to_do FROM clusterAllReplicas('default_cluster', system.mutations) WHERE is_done = 0;

#. Based on the query results in :ref:`3 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li14242152404310>`, confirm the table name related to the mutation task and try to clear the mutation task that has not been executed for a long time.

   **KILL MUTATION WHERE database =** *'Database name'* **AND table =** *'Table name'*\ **;**

   Or

   **KILL MUTATION WHERE database =** *'Database name'* **AND table =** *'Table name'* **AND mutation_id = 'mutation_id';**

   .. caution::

      alter table ... UPDATE and DELETE tasks are mutation tasks, which consume a large number of system resources and severely affect cluster performance. Do not frequently execute such tasks.

#. Wait for a while and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li6966662917>`.

**Check whether there is dirty data in the table.**

6. .. _alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li6966662917:

   Log in to the node for which the alarm is generated as user **root**. Check whether the **/var/log/Bigdata/clickhouse/clickhouseServer/clickhouse-server.log** file contains error messages like **Cannot parse xxx**.

   -  If yes, go to :ref:`7 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li169615662919>`.
   -  If no, go to :ref:`8 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li6769733151816>`.

7. .. _alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li169615662919:

   Check whether there is dirty data in the table where the mutation task is executed, which results in error message **Cannot parse xxx** during data parsing.

   -  If yes, clear the dirty data and perform :ref:`3 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li14242152404310>` again.
   -  If no, go to :ref:`8 <alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li6769733151816>`.

**Collect fault information.**

8.  .. _alm-45458__en-us_topic_0000002513714997_en-us_topic_0000002368412916_li6769733151816:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list and select **ClickHouse** for the target cluster.

10. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host and click **OK**.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
