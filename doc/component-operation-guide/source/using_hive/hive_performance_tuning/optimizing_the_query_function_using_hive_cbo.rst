:original_name: mrs_01_0983.html

.. _mrs_01_0983:

Optimizing the Query Function Using Hive CBO
============================================

Scenario
--------

When joining multiple tables in Hive, Hive supports Cost-Based Optimization (CBO). The system automatically selects the optimal plan based on the table statistics, such as the data volume and number of files, to improve the efficiency of joining multiple tables. Hive needs to collect table statistics before CBO optimization.

.. note::

   -  The CBO optimizes the joining sequence based on statistics and search criteria. However, the joining sequence may fail to be optimized in some special scenarios, such as data skew occurs and query condition values are not in the table.
   -  When column statistics collection is enabled, Reduce operations must be performed for aggregation. For insert tasks without the Reduce phase, Reduce operations will be performed to collect statistics.
   -  This section applies to MRS 3.\ *x* or later clusters.

Prerequisites
-------------

You have logged in to the Hive client. For details, see :ref:`Using a Hive Client <mrs_01_0952>`.

Procedure
---------

#. On the Manager UI, search for the **hive.cbo.enable** parameter in the service configuration of the Hive component, and select **true** to enable the function permanently.

#. Collect statistics about the existing data in Hive tables manually.

   Run the following command to manually collect statistics: Statistics about only one table can be collected. If statistics about multiple tables need to be collected, the command needs to be executed repeatedly.

   **ANALYZE TABLE [db_name.]tablename [PARTITION(partcol1[=val1], partcol2[=val2], ...)]**

   **COMPUTE STATISTICS**

   **[FOR COLUMNS]**

   **[NOSCAN];**

   .. note::

      -  When **FOR COLUMNS** is specified, column-level statistics are collected.
      -  When NOSCAN is specified, statistics about the file size and number of files will be collected, but specific files will not be scanned.

   For example:

   **analyze table table_name compute statistics;**

   **analyze table table_name compute statistics for columns;**

#. Configure the automatic statistics collection function of Hive. After the function is enabled, new statistics will be collected only when you insert data by running the **insert overwrite/into** command.

   -  Run the following commands on the Hive client to enable the statistics collection function temporarily:

      **set hive.stats.autogather = true;** enables the automatic collection of table/partition-level statistics.

      **set hive.stats.column.autogather = true;** enables the automatic collection of column-level statistics.

      .. note::

         -  The column-level statistics collection does not support complex data types, such as Map and Struct.
         -  The automatic table-level statistics collection does not support Hive on HBase tables.

   -  On the Manager UI, search for the **hive.stats.autogather** and **hive.stats.column.autogather** parameters in the service configuration of Hive, and select **true** to enable the collection function permanently.

#. Run the following command to view statistics:

   **DESCRIBE FORMATTED table_name[.column_name] PARTITION partition_spec;**

   For example:

   **desc formatted table_name;**

   **desc formatted table_name id;**

   **desc formatted table_name partition(time='2016-05-27');**

   .. note::

      Partition tables only support partition-level statistics collection, so you must specify partitions to query statistics for partition tables.
