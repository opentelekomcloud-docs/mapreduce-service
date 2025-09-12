:original_name: ALM-45447.html

.. _ALM-45447:

ALM-45447 ClickHouse Table Read-Only
====================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

The system checks the table status every minute. This alarm is generated when the system detects that a table is read-only. This alarm is automatically cleared when no table is read-only.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45447    Minor          Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

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

-  Data cannot be written to or modified.
-  Data synchronization in the replication table is interrupted, causing data inconsistency.

Possible Causes
---------------

The ZooKeeper is overloaded and metadata is lost.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address of the hostname in **Location**.

#. Log in to the node where the client is installed and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  Security mode (with Kerberos enabled):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance that reports the alarm* **--port** 21427 **--secure**

   -  Normal mode (with Kerberos disabled):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password** **--port** 21423

#. .. _alm-45447__li1399613358:

   Run the following SQL statement to check whether any table is in the read-only state:

   **select database,table from system.replicas where is_readonly = 1**

   -  If yes, go to :ref:`4 <alm-45447__li1735412272182>`.
   -  If no, go to :ref:`8 <alm-45447__li6871195733317>`.

#. .. _alm-45447__li1735412272182:

   Specify the database and table queried in :ref:`3 <alm-45447__li1399613358>` in the following statements and run them in sequence. Then, run the SQL statement in :ref:`3 <alm-45447__li1399613358>` and check whether the result contains any read-only table.

   **system restore replica** *database.table*\ **;**

   **system restart replica** *database.table*\ **;**

   -  If yes, go to :ref:`5 <alm-45447__li15308541181915>`.
   -  If no, go to :ref:`8 <alm-45447__li6871195733317>`.

#. .. _alm-45447__li15308541181915:

   Specify the database and table queried in :ref:`3 <alm-45447__li1399613358>` in the following statements and run them in sequence. Then, run the SQL statement in :ref:`3 <alm-45447__li1399613358>` and check whether the result contains the read-only table.

   **detach table** *database.table*\ **;**

   **attach table** *database.table*\ **;**

   -  If yes, go to :ref:`6 <alm-45447__li1481717455207>`.
   -  If no, go to :ref:`8 <alm-45447__li6871195733317>`.

#. .. _alm-45447__li1481717455207:

   Run the following SQL statement to view the structure information of the read-only table. In the statement, database and table are those queried in :ref:`3 <alm-45447__li1399613358>`.

   **show create table** *database.table*\ **;**

#. Run the following SQL statement to delete the read-only table and create a read-only table based on the table structure information in :ref:`6 <alm-45447__li1481717455207>`. Wait for several minutes, run the SQL statement in :ref:`3 <alm-45447__li1399613358>`, and check whether the result contains the read-only table.

   **drop database.table no delay;**

   -  If yes, go to :ref:`9 <alm-45447__li1314322683817>`.
   -  If no, go to :ref:`8 <alm-45447__li6871195733317>`.

   |image1|

#. .. _alm-45447__li6871195733317:

   Wait several minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45447__li1314322683817>`.

**Collect fault information.**

9.  .. _alm-45447__li1314322683817:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

11. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

12. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002381782666.png
