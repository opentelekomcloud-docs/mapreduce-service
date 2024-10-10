:original_name: ALM-45443.html

.. _ALM-45443:

ALM-45443 Slow SQL Queries in the Cluster
=========================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks slow SQL queries for ClickHouse every 1 minute. This alarm is generated when the execution time of a SQL statement is longer than or equal to the slow SQL threshold.

This alarm is automatically cleared when the system detects that the execution time of the SQL statement is shorter than the slow SQL threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45443    Major          Yes
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

Impact on the System
--------------------

The performance of the ClickHouse service deteriorates, which slows the response of other services. If there are too many slow SQL statements, the service may be unavailable.

Possible Causes
---------------

-  The ClickHouse service is overloaded.
-  The execution of SQL statements takes a long time.

Handling Procedure
------------------

**Check whether the ClickHouse service load is heavy.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--port** **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--user** *Username* **--password** **--port**

#. Run the following statement to check whether data is frequently written to the system table. If yes, wait until the service execution is complete and check whether the alarm is cleared.

   **SELECT query_id, user, FQDN(), elapsed, query FROM system.processes ORDER BY query_id;**

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45443__li1927623020184>`.

**Checking whether the SQL statements take a long time.**

4. .. _alm-45443__li1927623020184:

   Check the logical cluster to which the alarm object belongs. Log in to FusionInsight Manager, click **Cluster**, choose **Services** > **ClickHouse**, and click **Logic Cluster**. On the displayed page, choose **Query Management** > **Ongoing Slow Queries**. Check which SQL statements take a long time on the displayed page, confirm with the user to adjust services, optimize slow SQL statements, and check whether the optimization is successful.

   -  If yes, go to :ref:`5 <alm-45443__li1043716190409>`.
   -  If no, go to :ref:`6 <alm-45443__li6769733151816>`.

5. .. _alm-45443__li1043716190409:

   After the SQL statements are complete, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45443__li6769733151816>`.

**Collect fault information.**

6.  .. _alm-45443__li6769733151816:

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
