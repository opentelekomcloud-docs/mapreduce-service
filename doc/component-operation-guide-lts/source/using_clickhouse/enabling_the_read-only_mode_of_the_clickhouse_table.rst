:original_name: mrs_01_24451.html

.. _mrs_01_24451:

Enabling the Read-Only Mode of the ClickHouse Table
===================================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

During data migration, one-click balancing, decommissioning and capacity reduction, ClickHouse allows you to set the **only_allow_select_statement** parameter for MergeTree series tables to enable SELECT operations instead of ALTER, RENAME, DROP, and INSERT operations.

Procedure for Enabling the Read-Only Mode of the ClickHouse Table
-----------------------------------------------------------------

#. .. _mrs_01_24451__li10269200102512:

   Run the following commands to log in to the node where the client is installed as user **root**:

   **cd** *Client installation directory*

   **source bigdata_env**

#. Run the following command to authenticate the user if the cluster is in security mode (with Kerberos authentication enabled). Otherwise, skip this step.

   **kinit** *Component service user*

   .. note::

      The user must have the ClickHouse administrator permissions.

#. .. _mrs_01_24451__li4140746493:

   Run the proper client command to connect to the ClickHouse server.

   -  Normal mode

      **clickhouse client --host** *IP address of the ClickHouse instance*\ **--user** *Username* **--password** **--port** 9440 **--secure**

      *Enter the user password.*

   -  Security mode

      **clickhouse client --host** *IP address of the ClickHouse instance*\ **--port** 9440 **--secure**

   .. note::

      -  The user in normal mode is the default user, or you can create an administrator using the open source capability provided by the ClickHouse community. You cannot use the users created on FusionInsight Manager.
      -  To obtain the IP address of the ClickHouseServer instance, log in to FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse**, and click the **Instance** tab.

#. Run the following statement to set the table to read-only:

   **ALTER TABLE** *{table_name}* **MODIFY SETTING only_allow_select_statement = true;**

Disabling the Read-Only Mode of the Table
-----------------------------------------

#. Log in to the ClickHouse client by referring to :ref:`1 <mrs_01_24451__li10269200102512>` to :ref:`3 <mrs_01_24451__li4140746493>`.

#. Run the following statement to disable the read-only mode of the table:

   **ALTER TABLE** *{table_name}* **MODIFY SETTING only_allow_select_statement = false settings hw_internal_operation = true;**
