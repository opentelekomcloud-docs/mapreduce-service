:original_name: ALM-45456.html

.. _ALM-45456:

ALM-45456 ClickHouse Distributed DDL Task Not Completed Within Expected Time
============================================================================

.. note::

   This section applies only to MRS 3.6.0-LTS or later.

Alarm Description
-----------------

The system checks each ClickHouse node for distributed DDL tasks that have been running longer than the default threshold (600 seconds) every 5 minutes. This alarm is triggered when such tasks are detected. The execution timeout for distributed DDL tasks can be queried and adjusted using the **slow_ddl_cost_time** parameter in the ClickHouse service configuration.

This alarm is automatically cleared when the system detects that the execution time of tasks in the distributed DDL queue does not exceed the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45456    Major          Yes
======== ============== ============

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

If the ClickHouse service has a distributed DDL task that has not been completed for a long time, subsequent DDL tasks may be blocked, and metadata changes cannot be synchronized in the cluster in a timely manner.

Possible Causes
---------------

-  ClickHouseServer instance failure
-  Accumulated mutation tasks

Handling Procedure
------------------

**Check whether ClickHouseServer instances are faulty.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Choose **Cluster** > **Services** > **ClickHouse** > **Instances**, and check whether the ClickHouse instance associated with the alarm IP address is faulty.

   -  If yes, contact O&M personnel to restore the faulty ClickHouse instance and go to :ref:`3 <alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li2018114454020>`.
   -  If no, go to :ref:`4 <alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li9418193544015>`.

#. .. _alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li2018114454020:

   Wait several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li9418193544015>`.

**Check whether there are accumulated mutation tasks.**

4. .. _alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li9418193544015:

   Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user**\ *Username* **--password --port** 9440

5. .. _alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li11418535124017:

   Run the following statement to check the task type in **system.mutations** and check whether there is a mutation task that has not been executed for a long time (more than 10 minutes):

   .. code-block::

      select FQDN() as node, database, table, mutation_id, create_time, command, is_done, parts_to_do FROM clusterAllReplicas('default_cluster', system.mutations) WHERE is_done = 0;

6. Based on the query results in :ref:`5 <alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li11418535124017>`, confirm the table name related to the mutation task and try to clear the mutation task that has not been executed for a long time.

   **KILL MUTATION WHERE database = '**\ *Database name'* **AND table =** *'Table name'*\ **;**

   Or

   **KILL MUTATION WHERE database =** *'Database name'* **AND table =** *'Table name'* **AND mutation_id = 'mutation_id';**

   .. caution::

      alter table ... UPDATE and DELETE tasks are mutation tasks, which consume a large number of system resources and severely affect cluster performance. Do not frequently execute such tasks.

7. After the mutation task is cleared, wait for a while and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li6769733151816>`.

**Collect fault information.**

8.  .. _alm-45456__en-us_topic_0000002481515168_en-us_topic_0000002368253024_li6769733151816:

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
