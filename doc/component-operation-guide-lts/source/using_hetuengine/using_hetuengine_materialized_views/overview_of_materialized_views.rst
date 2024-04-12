:original_name: mrs_01_24541.html

.. _mrs_01_24541:

Overview of Materialized Views
==============================

Materialized Views applies to MRS 3.2.0 or later.

Background
----------

HetuEngine provides the materialized view capability. It enables you to pre-compute frequently accessed and time-consuming operators (such as join and aggregation operators) through materialized views. In this way, queries or subqueries that can match the materialized views are converted into corresponding materialized views, avoiding repeated data computing and improving the query response efficiency.

A materialized view is typically created based on the results of queries that aggregate and join multiple data tables.

Materialized views support query rewrite. It is an optimization technique that converts query statements compiled based on an original table into equivalent requests for querying one or more materialized view statements. The following is an example of the SQL statement of a materialized view:

.. code-block::

   create materialized view mv.default.mv1 with(mv_storage_table='hive.default.mv1') AS select id from hive.mvschema.t1;

The actual data of the materialized view is stored in the **hive.default.mv1** table. During query rewriting, the SQL statement **select id from hive.mvschema.t1** is rewritten as the table for querying the materialized view, that is, **select id from hive.default.mv1**.

Scenario
--------

Compared with common views, materialized views occupy storage resources and cause data delay because of actual data storage and pre-computation. Therefore, materialized views are recommended in the following scenarios:

-  Frequently executed queries are required.
-  Queries involve time-consuming operations like aggregation and join operations.
-  A certain delay is allowed for the query result data.
-  Materialized views can only be connected to co-deployed Hive and external Hive data sources. Data source tables are stored in ORC or PARQUET format. Cross-source and cross-domain scenarios are not supported.

Permission Introduction
-----------------------

:ref:`Table 1 <mrs_01_24541__en-us_topic_0000001520999729_table12606432191615>` lists materialized view permissions. Permission control for materialized views depends on the Ranger. If Ranger authentication is disabled, permissions may become invalid.

.. _mrs_01_24541__en-us_topic_0000001520999729_table12606432191615:

.. table:: **Table 1** HetuEngine materialized view permissions

   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Operation                                                                            | Permission on catalog mv  | Permission on Tables Stored in MVs | Permission on Original Physical Table |
   +======================================================================================+===========================+====================================+=======================================+
   | Creating a materialized view                                                         | Table creation permission | Table creation permission          | Column query permission               |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Deleting a materialized view                                                         | Table deletion permission | N/A                                | N/A                                   |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Refreshing a materialized view                                                       | Table update permission   | N/A                                | Column query permission               |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Overwriting query statements using materialized views                                | N/A                       | N/A                                | Column query permission               |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Using materialized views to rewrite the execution plan of query statements (EXPLAIN) | N/A                       | Column query permission            | Column query permission               |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Querying a materialized view                                                         | Column query permission   | N/A                                | N/A                                   |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Querying physical tables of materialized and non-materialized views                  | Column query permission   | N/A                                | Column query permission               |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Viewing a materialized view                                                          | N/A                       | N/A                                | N/A                                   |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+
   | Viewing the statement for creating a materialized view                               | N/A                       | N/A                                | N/A                                   |
   +--------------------------------------------------------------------------------------+---------------------------+------------------------------------+---------------------------------------+

How to Use
----------

.. table:: **Table 2** Introduction to materialized views

   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Phase                                                                 | Description                                                                                                                                                                                                                                                                               | Reference                                                                                   |
   +=======================================================================+===========================================================================================================================================================================================================================================================================================+=============================================================================================+
   | SQL statement example of materialized views                           | This section describes the operations supported by materialized views, including creating, listing, and querying materialized views.                                                                                                                                                      | :ref:`SQL Statement Example of Materialized Views <mrs_01_24545>`                           |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Configuring rewriting of materialized views                           | Enables the materialized view capability for faster query response.                                                                                                                                                                                                                       | :ref:`Configuring Rewriting of Materialized Views <mrs_01_24543>`                           |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Configuring recommendation of materialized views                      | Automatically learns and recommends materialized view SQL statements that are most valuable to services, improving online query efficiency and reducing system load pressure.                                                                                                             | :ref:`Configuring Recommendation of Materialized Views <mrs_01_24776>`                      |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Configuring caching of materialized views                             | The SQL statements that have been executed and rewritten for multiple times can be saved to the cache. When the SQL statements are executed again, the rewritten SQL statements are directly obtained from the cache instead of rewriting the SQL statements, improving query efficiency. | :ref:`Configuring Caching of Materialized Views <mrs_01_24544>`                             |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Configuring the validity period and data update of materialized views | -  Configures the validity period of the materialized view. Currently, only the materialized view within the validity period is automatically overwritten.                                                                                                                                | :ref:`Configuring the Validity Period and Data Update of Materialized Views <mrs_01_24546>` |
   |                                                                       | -  Configures periodic data update. Materialized views can be refreshed manually or automatically.                                                                                                                                                                                        |                                                                                             |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Configuring intelligent materialized views                            | Provides automatic creation of materialized views. You do not need to manually execute SQL statements to create materialized views (recommended).                                                                                                                                         | :ref:`Configuring Intelligent Materialized Views <mrs_01_24798>`                            |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Viewing automatic tasks of materialized views                         | Views the task execution status to evaluate the cluster health status.                                                                                                                                                                                                                    | :ref:`Viewing Automatic Tasks of Materialized Views <mrs_01_24505>`                         |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
