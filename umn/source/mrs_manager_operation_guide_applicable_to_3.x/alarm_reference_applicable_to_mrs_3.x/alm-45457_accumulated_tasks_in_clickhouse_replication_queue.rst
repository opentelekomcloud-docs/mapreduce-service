:original_name: ALM-45457.html

.. _ALM-45457:

ALM-45457 Accumulated Tasks in ClickHouse Replication Queue
===========================================================

.. note::

   This section applies only to MRS 3.6.0-LTS or later.

Alarm Description
-----------------

The alarm module checks the number of tasks in the replication queue of the ClickHouse service every 30 seconds. This alarm is generated when the alarm module detects that the number exceeds the threshold (50,000).

This alarm is cleared when the number of tasks falls below the threshold.

Alarm Attributes
----------------

+-----------------------+----------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                               | Auto Cleared          |
+=======================+==============================================+=======================+
| 45457                 | Critical (The default threshold is 100,000.) | Yes                   |
|                       |                                              |                       |
|                       | Major (The default threshold is 50,000.)     |                       |
+-----------------------+----------------------------------------------+-----------------------+

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

If there are tasks accumulated in the ClickHouse replication queue, the data synchronization for MergeTree tables may be delayed. This can also affect the subsequent write and mutation tasks, further increasing system load.

Possible Causes
---------------

-  Data is frequently written in small batches, causing the merge speed to lag behind the write speed.
-  There are a large number of mutation tasks in the cluster.
-  When a replica synchronization task is delayed for a long time, the system triggers the **Inconsistency Between ClickHouse Replicas** alarm in the cluster.

Handling Procedure
------------------

**Check whether data is written in small, high-frequency batches.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user**\ *Username* **--password --port** 9440

#. Run the following statements to check whether data is frequently written into the cluster in small batches.

   This query statement is used to analyze whether there are insert statements that write less than 1000 data records within 10 minutes in the ClickHouse cluster.

   .. code-block::

      SELECT user, query, count() AS insert_count, avg(written_rows) AS avg_rows_per_insert, min(event_time) AS first_time, max(event_time) AS last_time
      FROM clusterAllReplicas('default_cluster', system.query_log)
      WHERE (event_time >= (now() - toIntervalMinute(10))) AND (type = 'QueryFinish') AND (query_kind = 'Insert')
      GROUP BY user, query
      HAVING (insert_count >= 10) AND (avg_rows_per_insert < 10000)
      ORDER BY insert_count DESC;

   -  If yes, go to :ref:`4 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li35681216183116>`.
   -  If no, go to :ref:`5 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li1299583681514>`.

#. .. _alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li35681216183116:

   Limit or suspend services that perform high-frequency, small-batch writes. After the services are stopped, wait for several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li1299583681514>`.

**Check whether there are a large number of mutation tasks.**

5. .. _alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li1299583681514:

   Run the following statement to check whether the cluster contains a large number of mutation tasks:

   .. code-block::

      select FQDN() as node, database, table, mutation_id, create_time, command, is_done, parts_to_do FROM clusterAllReplicas('default_cluster', system.mutations) WHERE is_done = 0;

   -  If yes, go to :ref:`6 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li3995736191513>`.
   -  If no, go to :ref:`8 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li16102112161814>`.

6. .. _alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li3995736191513:

   Based on the query results in :ref:`5 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li1299583681514>`, confirm the table name related to the mutation task and try to clear the mutation task that has not been executed for a long time (more than 10 minutes).

   **KILL MUTATION WHERE database =** *'Database name'* **AND table =** *'Table name'*\ **;**

   Or

   **KILL MUTATION WHERE database =** *'Database name'* **AND table =** *'Table name'* **AND mutation_id = 'mutation_id';**

7. After the mutation task is cleared, wait for a while and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li16102112161814>`.

**Check whether ALM-45440 Inconsistency Between ClickHouse Replicas exists.**

8. .. _alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li16102112161814:

   Check whether **ALM-45440 Inconsistency Between ClickHouse Replicas** exists.

   -  If yes, go to :ref:`8 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li16102112161814>`.
   -  If no, go to :ref:`10 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li6769733151816>`.

9. Rectify the fault by following the handling procedure of **ALM-45440 Inconsistency Between ClickHouse Replicas**. Check whether the **ALM-45457 Accumulated Tasks in ClickHouse Replication Queue** alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li6769733151816>`.

**Collect fault information.**

10. .. _alm-45457__en-us_topic_0000002481675138_en-us_topic_0000002401972645_li6769733151816:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list and select **ClickHouse** for the target cluster.

12. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host and click **OK**.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
