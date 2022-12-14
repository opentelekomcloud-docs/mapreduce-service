:original_name: mrs_01_24200.html

.. _mrs_01_24200:

CREATE DATABASE: Creating a Database
====================================

This section describes the basic syntax and usage of the SQL statement for creating a ClickHouse database.

Basic Syntax
------------

**CREATE DATABASE [IF NOT EXISTS]** *Database_name* **[ON CLUSTER** *ClickHouse cluster name*\ **]**

.. note::

   The syntax **ON CLUSTER** *ClickHouse cluster name* enables the Data Definition Language (DDL) statement to be executed on all instances in the cluster at a time. You can run the following statement to obtain the cluster name from the **cluster** field:

   **select cluster,shard_num,replica_num,host_name from system.clusters;**

Example
-------

.. code-block::

   -- Create a database named test.
   CREATE DATABASE test ON CLUSTER default_cluster;
   -- After the creation is successful, run the query command for verification.
   show databases;
   ┌─name───┐
   │ default    │
   │ system     │
   │ test       │
   └──────┘
