:original_name: mrs_01_24201.html

.. _mrs_01_24201:

CREATE TABLE: Creating a Table
==============================

This section describes the basic syntax and usage of the SQL statement for creating a ClickHouse table.

Basic Syntax
------------

-  Method 1: Creating a table named **table_name** in the specified **database_name** database.

   If the table creation statement does not contain **database_name**, the name of the database selected during client login is used by default.

   **CREATE TABLE [IF NOT EXISTS]** *[database_name.]table_name* **[ON CLUSTER** *ClickHouse cluster name*\ **]**

   **(**

   *name1* **[**\ *type1*\ **] [DEFAULT\|MATERIALIZED\|ALIAS** *expr1*\ **],**

   *name2* **[**\ *type2*\ **] [DEFAULT\|MATERIALIZED\|ALIAS** *expr2*\ **],**

   **...**

   **)** *ENGINE* = *engine\_name()*

   [**PARTITION BY** *expr_list*]

   [**ORDER BY** *expr_list*]

   .. caution::

      You are advised to use **PARTITION BY** to create table partitions when creating a ClickHouse table. The ClickHouse data migration tool migrates data based on table partitions. If you do not use **PARTITION BY** to create table partitions during table creation, the table data cannot be migrated on the GUI in :ref:`Using the ClickHouse Data Migration Tool <mrs_01_24053>`.

-  Method 2: Creating a table with the same structure as **database_name2.table_name2** and specifying a different table engine for the table

   If no table engine is specified, the created table uses the same table engine as **database_name2.table_name2**.

   **CREATE TABLE [IF NOT EXISTS]** *[database_name.]table_name* **AS** [*database_name2*.]\ *table_name*\ 2 [ENGINE = *engine\_name*]

-  Method 3: Using the specified engine to create a table with the same structure as the result of the **SELECT** clause and filling it with the result of the **SELECT** clause

   **CREATE TABLE [IF NOT EXISTS]** *[database_name.]table_name* *ENGINE* = *engine\_name* **AS SELECT** ...

Example
-------

.. code-block::

   -- Create a table named test in the default database and default_cluster cluster.
   CREATE TABLE default.test ON CLUSTER default_cluster
   (
       `EventDate` DateTime,
       `id` UInt64
   )
   ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/default/test', '{replica}')
   PARTITION BY toYYYYMM(EventDate)
   ORDER BY id
