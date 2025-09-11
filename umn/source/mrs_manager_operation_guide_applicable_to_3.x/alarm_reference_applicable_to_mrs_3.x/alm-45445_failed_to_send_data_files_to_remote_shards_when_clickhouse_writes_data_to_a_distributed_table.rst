:original_name: ALM-45445.html

.. _ALM-45445:

ALM-45445 Failed to Send Data Files to Remote Shards When ClickHouse Writes Data to a Distributed Table
=======================================================================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

The ClickHouse instance checks the distributed table every 300 seconds. If the number of consecutive failures exceeds the threshold, an alarm is generated. In this case, the node where the ClickHouse instance writes data to the distributed table cannot send data files to remote shard nodes.

This alarm is cleared when the number of consecutive failures falls below the threshold.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45445    Major          Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

Alarm Changes
-------------

=========== ======= =========== =================
Change Type Version Description Reason for Change
=========== ======= =========== =================
New         3.3.1   New alarm   New alarm
=========== ======= =========== =================

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

The results of operations such as distributed table queries are abnormal.

Possible Causes
---------------

The status of some ClickHouse shard nodes is abnormal.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address of the hostname in **Location**.

#. .. _alm-45445__li49171056152620:

   Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password** **--port** 9000

#. .. _alm-45445__li1891825612618:

   Run the following SQL statement to obtain the shard based on the value of **data_path**. For example, if the value of **data_path** is **/srv/Bigdata/clickhouse/data1.../shard2_all_replicas**, the desired shard is **shard2**.

   **select database, table, data_path, data_files, error_count from system.distribution_queue where data_files != 0 and error_count != 0;**

#. .. _alm-45445__li611216137:

   Run the following SQL statement to obtain the node IP address (value of the **host** field in the system table **system.clusters**) of the shard where data fails to be sent to (**shard_num** obtained in :ref:`3 <alm-45445__li1891825612618>`):

   **select \* from system.clusters;**

#. Log in to the ClickHouse node (IP address obtained in :ref:`2 <alm-45445__li49171056152620>`) by referring to :ref:`4 <alm-45445__li611216137>`, run the following statement, and check whether the result can be returned:

   **SELECT 1;**

   If yes, go to :ref:`6 <alm-45445__li1522314306467>`.

   If no, go to :ref:`10 <alm-45445__li179191356102616>`.

#. .. _alm-45445__li1522314306467:

   Log in to the ClickHouse node (IP address obtained in :ref:`2 <alm-45445__li49171056152620>`) by referring to :ref:`4 <alm-45445__li611216137>`, run the following statement (**database_name** and **table_name** indicate the database name and table name of the local table corresponding to the distributed table):

   **select name,type from system.columns where database='**\ *database_name*\ **' and table='**\ *table_name*\ **'**

#. .. _alm-45445__li157331933114613:

   Log in to the ClickHouse node for which the alarm is generated by referring to :ref:`2 <alm-45445__li49171056152620>` and run the following statement (**database_name** and **table_name** indicate the database name and table name of the distributed table to which data is written):

   **select name,type from system.columns where database='**\ *database_name*\ **' and table='**\ *table_name*\ **'**

#. Check whether the results obtained in :ref:`6 <alm-45445__li1522314306467>` and :ref:`7 <alm-45445__li157331933114613>` are the same.

   If yes, go to :ref:`10 <alm-45445__li179191356102616>`.

   If no, ensure that the column information of the distributed table is consistent with that of the corresponding local table, and then try to write data to the distributed table.

#. Wait for several minutes and check whether the alarm is cleared.

   If yes, no further action is required.

   If no, go to :ref:`10 <alm-45445__li179191356102616>`.

**Collect fault information.**

10. .. _alm-45445__li179191356102616:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

12. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
