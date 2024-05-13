:original_name: mrs_01_248972.html

.. _mrs_01_248972:

Constraints on ClickHouseServer Scale-in
========================================

Cluster Scale
-------------

-  If a cluster has only one shard, the instance nodes cannot be removed from the cluster.

-  Multiple instance nodes in the same shard **must be decommissioned or recommissioned at the same time**.

   To query cluster shard information, perform the following steps:

   #. Log in to the node where the client is installed as the client installation user.

      **cd** *Client installation directory*

      **source bigdata_env**

      In security mode, run the following commands:

      **kinit** *ClickHouse service user*

      **clickhouse client --host** *IP address of the ClickHouse instance* **--port** **9440** **--secure**

      In normal mode, run the following command:

      **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *Username* **--password** **--port** *9000*

      *Enter the password.*

   #. Run the following command to query the cluster shard information:

      **select cluster,shard_num,replica_num,host_name from system.clusters;**

Cluster Storage
---------------

Ensure that the disk space of nodes that will not be decommissioned is sufficient for storing data of all decommissioned nodes. There must be approximately 10% redundant storage space after decommissioning to ensure that the remaining instances can run properly. The procedure is as follows:

#. Run the following command to check the disk usage on each node:

   **select \* from system.disks;**

   **free_space** indicates the free disk space, and **total_space** indicates the total disk space. The used space is calculated by subtracting the value of **free_space** from that of **total_space**, and its unit is byte.

#. Run the preceding command on a node you want to decommission and calculate the data volume on the node using the preceding formula.

#. Run the preceding command on a node that will not be decommissioned, and then use the following formula: (Value of **free_space** - Data volume of the node to be decommissioned)/Value of **total_space**. If the result is greater than 10%, the node can be decommissioned.

Cluster Status
--------------

If there is any faulty ClickHouseServer instance node in the cluster, all instance nodes in the cluster cannot be decommissioned. Log in to Manager, choose **Cluster** > **Services** > **ClickHouse**, click **Instance**, and view the running status of each node in the cluster.

Database
--------

If a database is deployed only on an instance node you want to decommission, the instance node cannot be decommissioned. To remove the instance node, you need to create the database on all ClickHouseServer instance nodes in the cluster. The procedure is as follows:

#. Run the **select \* from system.databases;** command to collect the database list of each node.

   **name** indicates the database name. **engine** indicates the database engine, and the default value is **Atomic**. If the default engine is used, you do not need to specify the engine when creating a table.

#. For the database deployed only on the instance node to be decommissioned, run the following command to create the database:

   **create database xxx engine=xxx on cluster xxx;**

Local Non-replicated Table
--------------------------

If a local non-replicated table is deployed only on an instance node you want to decommission, the instance node cannot be decommissioned. To decommission the node, create a local non-replicated table with the same name on any node that will not be decommissioned.

For example, the current cluster has two shards, shard 1 has two nodes A and B, and shard 2 has two nodes C and D. The non-replicated table **test** was created without the **ON CLUSTER** keyword, so the table is created only on node A.

In this case, to decommission nodes A and B in shard 1, you need to create the table **test** on node C or D in shard 2.

Run the following command to list the data tables of each node:

**select database,name,engine,create_table_query from system.tables where database != 'system';**

Perform the following operations according to the result:

-  Check the **engine** column. The table that does not contain the **Replicated** field is a local non-replicated table.

-  If there are no replicated tables on any nodes that will not be decommissioned, create one based the table created by **create_table_query**. The following creation statement is an example:

   **CREATE TABLE {database}.{table} ('column name' type...) ENGINE = MergeTree;**

Replicated Table
----------------

If a replicated table exists only on some nodes in the cluster, the nodes where the replicated table is deployed cannot be decommissioned. You need to manually create the replicated table on all instance nodes where no replicated table is deployed in the cluster before decommissioning.

For example, the current cluster has two shards, shard 1 has two nodes A and B, and shard 2 has two nodes C and D. The replicated table **test** was created without the **ON CLUSTER** keyword, so the table is created only on nodes A and B.

To decommission nodes A and B in shard 1, you need to create the table **test** on nodes C and D in shard 2.

Run the following command to list the data tables of each node:

**select database,name,engine,create_table_query from system.tables where database != 'system';**

Perform the following operations according to the result:

-  Check the **engine** column. The table that contains the **Replicated** field is a replicated table.
-  If there are no replicated tables on any nodes that will not be decommissioned, create one based the table created by **create_table_query**.

Distributed Table
-----------------

Distributed tables will not be migrated automatically for decommissioning. Create distributed tables on the nodes that will not be decommissioned.

Run the following command to list data tables of each node and check the **engine** column. These tables are distributed tables if this column contains field **Distributed**.

**select database,name,engine from system.tables where database != 'system';**

.. note::

   Creating distributed tables on these nodes will not affect the decommissioning, but may affect subsequent service operations.

View
----

Views will not be automatically migrated for decommissioning, and views do not store data. Run the following command to list data tables of each node and check the **engine** column. These tables are views if this column contains field **View**.

**select database,name,engine from system.tables where database != 'system';**

Run the following command to delete the views one by one:

**drop view {database_name}.{table_name};**

Materialized Views
------------------

Materialized views will not be automatically migrated for Decommissioning. Create materialized views on the nodes that will not be decommissioned. If the materialized view of a node to be decommissioned does not display the specified aggregation table but uses an embedded table, the node cannot be decommissioned.

Run the following command to list data tables of each node and check the **engine** column. These tables are materialized views if this column contains field **MaterializedView**.

**select database,name,engine,** **create_table_query from system.tables where database != 'system';**

The table whose **create_table_query** column contains the **POPULATE** field is an embedded table. Views are initialized when they are created, and newly inserted data is ignored during the initialization. A table that does not contain the **POPULATE** field is an aggregation table. Newly inserted data is directly inserted into the view charts and support tables, and the original data is manually loaded into the views and support tables. The table creation operations of the aggregation table and embedded table are different.

Perform the following operations to process the materialized views of the node to be decommissioned:

#. Record the materialized views and delete them.

   **drop view {database_name}.{table_name};**

#. After the node decommissioning is complete, delete and recreate the corresponding materialized views on in-use nodes to update the materialized views.

#. To create an aggregation table, specify **WHERE** to search for historical data and manually import the historical data to the materialized views. Otherwise, historical data cannot be imported to the materialized views based on unified conditions. As a result, data is imported repeatedly. For example, an update point can be specified to ensure that data before the update point is manually loaded in **INSERT** mode.

   -  Add **WHERE** *{* *Time field (for example, date)}*\ **>= toDate** **(**\ *{ Current time (for example, '2022-12-01 00:00:00')}*\ **)** to the table creation statement.
   -  **insert into** *{table}* **select** *{Table field}* **from** *{Source table}* **where** *{Time field}*\ **< toDate** *({Current time})* is used to load original data.

#. Embedded tables will lose data generated during table creation. You can specify **WHERE** to filter out all historical data. In this case, an empty table is created, and you only need to manually insert all data in the historical data source table.

Tables of Third-Party Engines
-----------------------------

Currently, tables of third-party engines cannot be automatically migrated for decommissioning.

Run the following command to list data tables of each node and check the **engine** column. These tables are tables of third-party engines if this column does not contain any of the following fields: **MergeTree**, **View**, **MaterializedView**, **Distributed**, and **Log**. (The **engine** column of a third-party engine table may contain field **Memory**, **HDFS**, or **MySQL**.)

**select database,name,engine from system.tables where database != 'system';**

Create third-party engine tables on the nodes that will not be decommissioned and delete those from the nodes that will be decommissioned.

Detached Data
-------------

If the table on a node to be decommissioned has been detached and data still exists in the **detached** directory, the node cannot be decommissioned. You need to attach the data in the **detached** directory to other directories before decommissioning.

#. Run the following command to view the **system.detached_parts** system catalog of the node to be decommissioned:

   **select \* from system.detached_parts;**

#. If **detached part** data exists and these partitions are no longer used, run the following command to delete the **detached part** data:

   **ALTER TABLE {table_name} DROP DETACHED PARTITION {partition_expr} SETTINGS allow_drop_detached = 1;**

#. Run the following command to check whether there is any **detached part** data in the **system.detached_parts** system catalog:

   **select \* from system.detached_parts;**

   If the command output is empty, there is no **detached part** data in this system catalog.
