:original_name: ALM-45454.html

.. _ALM-45454:

ALM-45454 ClickHouse Has Tables with Too Frequent Data Writes
=============================================================

.. note::

   This section applies only to MRS 3.5.1 and later versions.

Alarm Description
-----------------

The system checks whether ClickHouse nodes have tables with high write frequency within the previous day every day. This alarm is generated when the system detects such tables. You can view and adjust the write frequency threshold by setting the **MAX_INSERT_NUMBER_PER_SECOND** parameter of the ClickHouse service.

This alarm is automatically cleared when the system detects that there is no table with high write frequency on ClickHouse nodes on the previous day.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45454    Major          Yes
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

If data is written into tables too frequently, the system may become overloaded and the write operations may even fail.

Possible Causes
---------------

Batch write is not implemented for the service.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password --port** 9440

#. .. _alm-45454__en-us_topic_0000002513714995_en-us_topic_0000002215910673_li14242152404310:

   Run the following statement to query the tables with high write frequency:

   **select tables, cnt from (with toStartOfInterval(event_time,toIntervalSecond(600)) As time\_ SELECT time\_ , tables, count() as cnt FROM system.query_log WHERE type='QueryFinish' and query_kind = 'Insert' and event_date = '${alarm_date}' GROUP BY time_, tables) where cnt >= (${MAX_INSERT_NUMBER_PER_SECOND} \* 600);**

   .. note::

      -  **alarm_date**: the day before the alarm is generated. For example, if the alarm is generated on February 20, 2025, the value is **2025-02-19**.
      -  **MAX_INSERT_NUMBER_PER_SECOND**: write frequency threshold. To obtain the threshold, log in to MRS Manager and choose **Cluster** > **Services** > **ClickHouse** > **Configurations** > **All Configurations**.

#. Optimize the service logic based on the results obtained in :ref:`3 <alm-45454__en-us_topic_0000002513714995_en-us_topic_0000002215910673_li14242152404310>`.

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
