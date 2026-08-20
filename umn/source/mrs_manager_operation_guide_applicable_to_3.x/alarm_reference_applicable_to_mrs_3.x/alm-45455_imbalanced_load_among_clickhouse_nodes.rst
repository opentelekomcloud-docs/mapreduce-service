:original_name: ALM-45455.html

.. _ALM-45455:

ALM-45455 Imbalanced Load Among ClickHouse Nodes
================================================

.. note::

   This section applies only to MRS 3.5.1 and later versions.

Alarm Description
-----------------

The system checks the number of query requests received on the previous day by each ClickHouse node every day. This alarm is generated when the query requests among ClickHouse nodes are imbalanced. You can view and adjust the threshold for the gap between query requests received by these ClickHouse nodes by setting the **MAX_NODE_BALANCE_THRESHOLD** parameter of the ClickHouse service.

This alarm is automatically cleared when the system detects that the query requests received by all ClickHouse nodes on the previous day are balanced.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45455    Major          Yes
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

If the load among ClickHouse nodes is imbalanced, some nodes may be highly overloaded, and the cluster performance may be unstable, affecting normal service running.

Possible Causes
---------------

The load balancing component or service is not used.

Handling Procedure
------------------

**Check whether the ClickHouse service is overloaded.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password --port** 9440

#. Run the following statement to query the number of query requests received by each node:

   **select FQDN(), count() as cnt from clusterAllReplicas(${cluster_name}, 'system.query_log') where query_kind = 'Select' and type = 'QueryStart' and user != 'clickhouse' and event_date = '${alarm_date}' group by FQDN();**

   .. note::

      -  **cluster_name**: cluster name. The default value is **default_cluster**.
      -  **alarm_date**: the day before the alarm is generated. For example, if the alarm is generated on February 20, 2025, the value is **2025-02-19**.

#. Check whether the load balancing component or service is used. If not, optimize the service logic.

**Collect fault information.**

5. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
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
