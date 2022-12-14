:original_name: mrs_01_24292.html

.. _mrs_01_24292:

Backing Up and Restoring ClickHouse Data Using a Data File
==========================================================

Scenario
--------

This section describes how to back up data by exporting ClickHouse data to a CSV file and restore data using the CSV file.

Prerequisites
-------------

-  You have installed the ClickHouse client.
-  You have created a user with related permissions on ClickHouse tables on Manager.
-  You have prepared a server for backup.

Backing Up Data
---------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create ClickHouse tables. If Kerberos authentication is disabled for the current cluster, skip this step.

   a. Run the following command if it is an MRS 3.1.0 cluster:

      **export CLICKHOUSE_SECURITY_ENABLED=true**

   b. **kinit** *Component service user*

      Example: **kinit clickhouseuser**

#. Run the ClickHouse client command to export the ClickHouse table data to be backed up to a specified directory.

   **clickhouse client --host** *Host name/Instance IP address* **--secure --port 9440 --query=**"*Table query statement*" > *Path of the exported CSV file*

   The following shows an example of backing up data in the **test** table to the **default_test.csv** file on the ClickHouse instance **10.244.225.167**.

   **clickhouse client --host 10.244.225.167 --secure --port 9440 --query="select \* from default.test FORMAT CSV" > /opt/clickhouse/default_test.csv**

#. Upload the exported CSV file to the backup server.

Restoring Data
--------------

#. Upload the backup data file on the backup server to the directory where the ClickHouse client is located.

   For example, upload the **default_test.csv** backup file to the **/opt/clickhouse** directory.

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create ClickHouse tables. If Kerberos authentication is disabled for the current cluster, skip this step.

   a. Run the following command if it is an MRS 3.1.0 cluster:

      **export CLICKHOUSE_SECURITY_ENABLED=true**

   b. **kinit** *Component service user*

      Example: **kinit clickhouseuser**

#. Run the ClickHouse client command to log in to the ClickHouse cluster.

   **clickhouse client --host** *Host name/Instance IP address* **--secure** **--port 9440**

#. .. _mrs_01_24292__li14929104515101:

   Create a table with the format corresponding to the CSV file.

   **CREATE TABLE [IF NOT EXISTS]** *[database_name.]table_name* **[ON CLUSTER** *Cluster name*\ **]**

   **(**

   *name1* **[**\ *type1*\ **] [DEFAULT\|**\ *materialized*\ **\|ALIAS** *expr1*\ **],**

   *name2* **[**\ *type2*\ **] [DEFAULT\|**\ *materialized*\ **\|ALIAS** *expr2*\ **],**

   **...**

   **)** *ENGINE* = *engine*

#. Import the content in the backup file to the table created in :ref:`7 <mrs_01_24292__li14929104515101>` to restore data.

   **clickhouse client --host** *Host name/Instance IP address* **--secure --port 9440 --query=**"**insert into** *Table name* **FORMAT CSV**" **<** *CSV file path*

   The following shows an example of restoring data from the **default_test.csv** backup file to the **test_cpy** table on the ClickHouse instance **10.244.225.167**.

   **clickhouse client --host** **10.244.225.167** **--secure --port 9440 --query="insert into default.test_cpy FORMAT CSV" < /opt/clickhouse/default_test.csv**
