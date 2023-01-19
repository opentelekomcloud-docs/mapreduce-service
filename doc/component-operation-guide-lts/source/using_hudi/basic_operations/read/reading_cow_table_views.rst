:original_name: mrs_01_24098.html

.. _mrs_01_24098:

Reading COW Table Views
=======================

-  Reading the real-time view (using Hive and SparkSQL as an example): Directly read the Hudi table stored in Hive.

   .. code-block::

      select count(*) from test;

-  Reading the real-time view (using the Spark DataSource API as an example): This is similar to reading a common DataSource table.

   **QUERY_TYPE_OPT_KEY** must be set to **QUERY_TYPE_SNAPSHOT_OPT_VAL**.

   .. code-block::

      spark.read.format("hudi")
      .option(QUERY_TYPE_OPT_KEY, QUERY_TYPE_SNAPSHOT_OPT_VAL) // Set the query type to the real-time view.
      .load("/tmp/default/cow_bugx/*/*/*/*") // Set the path of the Hudi table to be read. The current table has three levels of partitions.
      .createTempView("mycall")
      spark.sql("select * from mycall").show(100)

-  Reading the incremental view (using Hive and SparkSQL as an example):

   .. code-block::

      set hoodie.test.consume.mode=INCREMENTAL;  // Specify the incremental reading mode.
      set hoodie.test.consume.max.commits=3;  // Specify the maximum number of commits to be consumed.
      set hoodie.test.consume.start.timestamp=20201227153030;  // Specify the initial incremental pull commit.
      select count(*) from default.test where `_hoodie_commit_time`>'20201227153030'; // This filtering condition must be added, and the value is the initial incremental pull commit.

-  Reading the incremental view (using the Spark DataSource API as an example):

   **QUERY_TYPE_OPT_KEY** must be set to **QUERY_TYPE_INCREMENTAL_OPT_VAL**.

   .. code-block::

      spark.read.format("hudi")
      .option(QUERY_TYPE_OPT_KEY, QUERY_TYPE_INCREMENTAL_OPT_VAL) // Set the query type to the incremental mode.
      .option(BEGIN_INSTANTTIME_OPT_KEY, "20210308212004")  // Specify the initial incremental pull commit.
      .option(END_INSTANTTIME_OPT_KEY, "20210308212318")  //: Specify the end commit of the incremental pull.
      .load("/tmp/default/cow_bugx/*/*/*/*")  // Set the path of the Hudi table to be read. The current table has three levels of partitions.
      .createTempView("mycall")  // Register as a Spark temporary table.
      spark.sql("select * from mycall where `_hoodie_commit_time`>'20210308211131'")// Start the query. The statement is the same as the Hive incremental query statement.
      .show(100, false)

-  Reading the read-optimized view: The read-optimized view of COW tables is equivalent to the real-time view.
