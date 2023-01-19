:original_name: mrs_01_24099.html

.. _mrs_01_24099:

Reading MOR Table Views
=======================

After the MOR table is synchronized to Hive, the following two tables are synchronized to Hive: *Table name*\ **\_rt** and *Table name*\ **\_ro**. The table suffixed with **rt** indicates the real-time view, and the table suffixed with **ro** indicates the read-optimized view. For example, the name of the Hudi table to be synchronized to Hive is **test**. After the table is synchronized to Hive, two more tables **test_rt** and **test_ro** are generated in the Hive table.

-  Reading the real-time view (using Hive and SparkSQL as an example): Directly read the Hudi table with suffix **\_rt** stored in Hive.

   .. code-block::

      select count(*) from test_rt;

-  Reading the real-time view (using the Spark DataSource API as an example): The operations are the same as those for the COW table. For details, see the operations for the COW table.

-  Reading the incremental view (using Hive and SparkSQL as an example):

   .. code-block::

      set hive.input.format=org.apache.hudi.hadoop.hive.HoodieCombineHiveInputFormat; // This parameter does not need to be specified for SparkSQL.
      set hoodie.test.consume.mode=INCREMENTAL;
      set hoodie.test.consume.max.commits=3;
      set hoodie.test.consume.start.timestamp=20201227153030;
      select count(*) from default.test_rt where `_hoodie_commit_time`>'20201227153030';

-  Incremental view (using the Spark DataSource API as an example): The operations are the same as those for the COW table. For details, see the operations for the COW table.

-  Reading the read-optimized view (using Hive and SparkSQL as an example): Directly read the Hudi table with suffix **\_ro** stored in Hive.

   .. code-block::

      select count(*) from test_ro;

-  Reading the read-optimized view (using the Spark DataSource API as an example): This is similar to reading a common DataSource table.

   **QUERY_TYPE_OPT_KEY** must be set to **QUERY_TYPE_READ_OPTIMIZED_OPT_VAL**.

   .. code-block::

      spark.read.format("hudi")
      .option(QUERY_TYPE_OPT_KEY, QUERY_TYPE_READ_OPTIMIZED_OPT_VAL) // Set the query type to the read-optimized view.
      .load("/tmp/default/mor_bugx/*/*/*/*") // Set the path of the Hudi table to be read. The current table has three levels of partitions.
      .createTempView("mycall")
      spark.sql("select * from mycall").show(100)
      Note:
      Spark SQL cannot query the incremental view of the datasource table but can query Hive tables and dataSource APIs.
