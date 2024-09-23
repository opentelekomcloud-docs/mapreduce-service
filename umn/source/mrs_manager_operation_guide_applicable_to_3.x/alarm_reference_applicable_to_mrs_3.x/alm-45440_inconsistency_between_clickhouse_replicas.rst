:original_name: ALM-45440.html

.. _ALM-45440:

ALM-45440 Inconsistency Between ClickHouse Replicas
===================================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

When the number of ClickHouse replicas is greater than 1, the system periodically checks the replicated table. This alarm is generated if replicated table data is not synchronized. This alarm is cleared when data in all replicated tables between replicas becomes synchronized.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45440    Minor          Yes
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
| Table       | Specifies the table name for which the alarm is generated.        |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The data reliability of the ClickHouse replicated table is affected, causing data differences and affecting the query result of the distributed table.

Possible Causes
---------------

-  The ClickHouse service is overloaded.
-  The connection between the ClickHouse and ZooKeeper is abnormal.

Handling Procedure
------------------

**Check whether the ClickHouse service load is heavy.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and view the database name, table name, role name and IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--user** *Username* **--password** **--port** 9000

#. Run the following statement to check whether data is frequently written to the system table. If yes, wait until the service execution is complete and check whether the alarm is cleared.

   **SELECT query_id, user, FQDN(), elapsed, query FROM system.processes ORDER BY query_id;**

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45440__li99531855012>`.

#. .. _alm-45440__li99531855012:

   Check whether a large amount of data is written. If yes, wait until the task is complete and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45440__li99531451701>`.

#. .. _alm-45440__li99531451701:

   Run the following statement to check whether replicas are synchronized:

   **select table,absolute_delay, queue_size, inserts_in_queue, merges_in_queue from system.replicas where absolute_delay > 0 order by absolute_delay desc limit 10;**

   -  If yes, go to :ref:`6 <alm-45440__li595425809>`.
   -  If no, go to :ref:`9 <alm-45440__li1927623020184>`.

#. .. _alm-45440__li595425809:

   If **inserts_in_queue** contains a large amount of content to be inserted, run the following SQL statement to query the replica synchronization queue and locate the error cause:

   **SELECT database,table,type,any(last_exception),any(postpone_reason),min(create_time),max(last_attempt_time),max(last_postpone_time),max(num_postponed) AS max_postponed,max(num_tries) AS max_tries,min(num_tries) AS min_tries,countIf(last_exception != '') AS count_err,countIf(num_postponed > 0) AS count_postponed,countIf(is_currently_executing) AS count_executing,count() AS count_all FROM system.replication_queue GROUP BY database,table,type ORDER BY count_all DESC**

   Check whether an error message similar to the following is displayed:

   .. code-block::

      Not executing fetch of part xxx because n fetches already executing, max n

   -  If yes, go to :ref:`7 <alm-45440__li1295605909>`.
   -  If no, go to :ref:`9 <alm-45440__li1927623020184>`.

#. .. _alm-45440__li1295605909:

   On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse** > **Configurations** > **All Configurations**, and check whether the value of **background_pool_size** is twice the number of cores on the node.

   -  If yes, go to :ref:`9 <alm-45440__li1927623020184>`.
   -  If no, go to :ref:`8 <alm-45440__li69571258018>`.

#. .. _alm-45440__li69571258018:

   Set this parameter to twice the number of cores on the node and synchronize the configuration. Wait for a while and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45440__li1927623020184>`.

**Check the connectivity between ClickHouse and ZooKeeper.**

9.  .. _alm-45440__li1927623020184:

    Log in to the node where the ClickHouseServer instance is located, go to **${BIGDATA_HOME}/FusionInsight_ClickHouse_*/*_*_ClickHouseServer/etc**, and check whether the port numbers of the ClickHouseServer and ZooKeeper in the **config.xml** file are the same, as shown in the following information in bold:

    .. note::

       To view the ZooKeeper port number, choose **Cluster** > **Services** > **ZooKeeper** > **Configurations** > **All Configurations** on FusionInsight Manager, and check the value of **clientPort**.

    .. code-block::

         <zookeeper>
           <session_timeout_ms>10000</session_timeout_ms>
           <node index="1">
             <host>server-2110082001-0019</host>
             <port>24002</port>
           </node>
           <node index="2">
             <host>server-2110082001-0018</host>
             <port>24002</port>
           </node>
           <node index="3">
             <host>server-2110082001-0017</host>
             <port>24002</port>
           </node>
        </zookeeper>

    -  If yes, go to :ref:`11 <alm-45440__li6769733151816>`.
    -  If no, go to :ref:`10 <alm-45440__li142761430201810>`.

10. .. _alm-45440__li142761430201810:

    Change the port number to the ZooKeeper port number, restart the ClickHouseServer instance, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-45440__li6769733151816>`.

**Collect fault information.**

11. .. _alm-45440__li6769733151816:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

13. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

14. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

15. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
