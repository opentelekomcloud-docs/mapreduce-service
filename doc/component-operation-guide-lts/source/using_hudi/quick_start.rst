:original_name: mrs_01_24033.html

.. _mrs_01_24033:

Quick Start
===========

Scenario
--------

This section describes capabilities of Hudi using spark-shell. Using the Spark data source, this section describes how to insert and update a Hudi dataset of the default storage mode Copy-on Write (COW) tables based on code snippets. After each write operation, you will be introduced how to read snapshot and incremental data.

Prerequisites
-------------

-  You have downloaded and installed the Hudi client. Currently, Hudi is integrated in Spark2x. You only need to download the Spark2x client on Manager. For example, the client installation directory is **/opt/client**.
-  You have created a user and added the user to user groups **hadoop** and **hive** on Manager.

Procedure
---------

#. Download and install the Hudi client. For details, see :ref:`Using an MRS Client <mrs_01_0787>`.

   .. note::

      Currently, Hudi is integrated in Spark2x. You only need to download the Spark2x client on Manager. For example, the client installation directory is **/opt/client**.

#. Log in to the node where the client is installed as user **root** and run the following command:

   **cd /opt/client**

#. Run the following commands to load environment variables:

   **source bigdata_env**

   **source Hudi/component_env**

   **kinit** *Created user*

   .. note::

      -  You need to change the password of the created user, and then run the **kinit** command to log in to the system again.
      -  In normal mode, you do not need to run the **kinit** command.

#. Use **spark-shell --master yarn-client** to import Hudi packages to generate test data:

   .. code-block::

      // Import required packages.
      import org.apache.hudi.QuickstartUtils._
      import scala.collection.JavaConversions._
      import org.apache.spark.sql.SaveMode._
      import org.apache.hudi.DataSourceReadOptions._
      import org.apache.hudi.DataSourceWriteOptions._
      import org.apache.hudi.config.HoodieWriteConfig._
      // Define the storage path and generate the test data.
      val tableName = "hudi_cow_table"
      val basePath = "hdfs://hacluster/tmp/hudi_cow_table"
      val dataGen = new DataGenerator
      val inserts = convertToStringList(dataGen.generateInserts(10))
      val df = spark.read.json(spark.sparkContext.parallelize(inserts, 2))

#. Write data to the Hudi table in overwrite mode.

   **df.write.format("org.apache.hudi").**

   **options(getQuickstartWriteConfigs).**

   **option(PRECOMBINE_FIELD_OPT_KEY, "ts").**

   **option(RECORDKEY_FIELD_OPT_KEY, "uuid").**

   **option(PARTITIONPATH_FIELD_OPT_KEY, "partitionpath").**

   **option(TABLE_NAME, tableName).**

   **mode(Overwrite).**

   **save(basePath)**

#. Query the Hudi table.

   Register a temporary table and query the table.

   **val roViewDF = spark.**

   **read.**

   **format("org.apache.hudi").**

   **load(basePath + "/*/*/*/*")**

   **roViewDF.createOrReplaceTempView("hudi_ro_table")**

   **spark.sql("select fare, begin_lon, begin_lat, ts from hudi_ro_table where fare > 20.0").show()**

#. Generate new data and update the Hudi table in append mode.

   **val updates = convertToStringList(dataGen.generateUpdates(10))**

   **val df = spark.read.json(spark.sparkContext.parallelize(updates, 1))**

   **df.write.format("org.apache.hudi").**

   **options(getQuickstartWriteConfigs).**

   **option(PRECOMBINE_FIELD_OPT_KEY, "ts").**

   **option(RECORDKEY_FIELD_OPT_KEY, "uuid").**

   **option(PARTITIONPATH_FIELD_OPT_KEY, "partitionpath").**

   **option(TABLE_NAME, tableName).**

   **mode(Append).**

   **save(basePath)**

#. Query incremental data in the Hudi table.

   -  Reload data.

      **spark.**

      **read.**

      **format("org.apache.hudi").**

      **load(basePath + "/*/*/*/*").**

      **createOrReplaceTempView("hudi_ro_table")**

   -  Perform the incremental query.

      **val commits = spark.sql("select distinct(_hoodie_commit_time) as commitTime from hudi_ro_table order by commitTime").map(k => k.getString(0)).take(50)**

      **val beginTime = commits(commits.length - 2)**

      **val incViewDF = spark.**

      **read.**

      **format("org.apache.hudi").**

      **option(VIEW_TYPE_OPT_KEY, VIEW_TYPE_INCREMENTAL_OPT_VAL).**

      **option(BEGIN_INSTANTTIME_OPT_KEY, beginTime).**

      **load(basePath);**

      **incViewDF.registerTempTable("hudi_incr_table")**

      **spark.sql("select \`_hoodie_commit_time`, fare, begin_lon, begin_lat, ts from hudi_incr_table where fare > 20.0").show()**

#. Perform the point-in-time query.

   **val beginTime = "000"**

   **val endTime = commits(commits.length - 2)**

   **val incViewDF = spark.read.format("org.apache.hudi").**

   **option(VIEW_TYPE_OPT_KEY, VIEW_TYPE_INCREMENTAL_OPT_VAL).**

   **option(BEGIN_INSTANTTIME_OPT_KEY, beginTime).**

   **option(END_INSTANTTIME_OPT_KEY, endTime).**

   **load(basePath);**

   **incViewDF.registerTempTable("hudi_incr_table")**

   **spark.sql("select \`_hoodie_commit_time`, fare, begin_lon, begin_lat, ts from hudi_incr_table where fare > 20.0").show()**

#. Delete data.

   -  Prepare the data to be deleted.

      **val df = spark.sql("select uuid, partitionpath from hudi_ro_table limit 2")**

      **val deletes = dataGen.generateDeletes(df.collectAsList())**

   -  Execute the deletion.

      **val df = spark.read.json(spark.sparkContext.parallelize(deletes, 2));**

      **df.write.format("org.apache.hudi").**

      **options(getQuickstartWriteConfigs).**

      **option(OPERATION_OPT_KEY,"delete").**

      **option(PRECOMBINE_FIELD_OPT_KEY, "ts").**

      **option(RECORDKEY_FIELD_OPT_KEY, "uuid").**

      **option(PARTITIONPATH_FIELD_OPT_KEY, "partitionpath").**

      **option(TABLE_NAME, tableName).**

      **mode(Append).**

      **save(basePath);**

   -  Query data again.

      **val roViewDFAfterDelete = spark.**

      **read.**

      **format("org.apache.hudi").**

      **load(basePath + "/*/*/*/*")**

      **roViewDFAfterDelete.createOrReplaceTempView("hudi_ro_table")**

      **spark.sql("select uuid, partitionPath from hudi_ro_table").show()**
