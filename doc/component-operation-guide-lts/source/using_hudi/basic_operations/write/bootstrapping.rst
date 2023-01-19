:original_name: mrs_01_24069.html

.. _mrs_01_24069:

Bootstrapping
=============

The bootstrapping function provided by Hudi converts historical tables into Hudi tables without any change by generating Hoodie management files based on historical Parquet tables.

The following shows an example of converting a Hive table in the **hdfs://hacluster/user/hive/warehouse/pq1 directory** on HDFS to a Hudi table and save it in the **hdfs://hacluster/tmp/hudi_bootstrap_test** directory.

.. note::

   -  Bootstrapping and write operations cannot be executed concurrently. Bootstrapping is used only to creat new Hudi tables rather to execute existing Hudi tables.
   -  Bootstrapping supports only the write operations on COW tables.

.. code-block::

   spark-shell

   import collection.JavaConverters._
   import org.apache.hadoop.fs.FileSystem
   import org.apache.hudi.bootstrap.SparkParquetBootstrapDataProvider
   import org.apache.hudi.client.bootstrap.selector.FullRecordBootstrapModeSelector
   import org.apache.hudi.{DataSourceReadOptions, DataSourceWriteOptions, HoodieDataSourceHelpers}
   import org.apache.hudi.common.fs.FSUtils
   import org.apache.hudi.common.table.timeline.HoodieTimeline
   import org.apache.hudi.config.{HoodieBootstrapConfig, HoodieCompactionConfig, HoodieWriteConfig}
   import org.apache.hudi.keygen.SimpleKeyGenerator
   import org.apache.spark.api.java.JavaSparkContext
   import org.apache.spark.sql.functions.{col, lit}
   import org.apache.spark.sql.{SaveMode, SparkSession}
   import org.apache.hudi.QuickstartUtils._
   import scala.collection.JavaConversions._
   import org.apache.spark.sql.SaveMode._
   import org.apache.hudi.DataSourceReadOptions._
   import org.apache.hudi.DataSourceWriteOptions._
   import org.apache.hudi.config.HoodieWriteConfig._
   import java.time._
   import java.util.Collections

   val timestamp = Instant.now.toEpochMilli
   val jsc = JavaSparkContext.fromSparkContext(spark.sparkContext)
   val numRecords: Int = 100
   val srcPath = "hdfs://hacluster/user/hive/warehouse/pq1"
   val basePath = "hdfs://hacluster/tmp/hudi_bootstrap_test"

   // Hudi configuration information
   val commonOpts: Map[String, String] = Map(
       HoodieWriteConfig.INSERT_PARALLELISM -> "4",
       HoodieWriteConfig.UPSERT_PARALLELISM -> "4",
       HoodieWriteConfig.DELETE_PARALLELISM -> "4",
       HoodieWriteConfig.BULKINSERT_PARALLELISM -> "4",
       HoodieWriteConfig.FINALIZE_WRITE_PARALLELISM -> "4",
       HoodieBootstrapConfig.BOOTSTRAP_PARALLELISM -> "4",
       DataSourceWriteOptions.RECORDKEY_FIELD_OPT_KEY -> "col1",
       DataSourceWriteOptions.PARTITIONPATH_FIELD_OPT_KEY -> "partition",
       DataSourceWriteOptions.PRECOMBINE_FIELD_OPT_KEY -> "timestamp",
       HoodieWriteConfig.TABLE_NAME -> "hoodie_test"
     )
   // Bootstrapping
   val bootstrapDF = spark.emptyDataFrame
   bootstrapDF.write.
     format("hudi").
     options(commonOpts).
     option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.BOOTSTRAP_OPERATION_OPT_VAL).
     option(DataSourceWriteOptions.TABLE_TYPE_OPT_KEY, DataSourceWriteOptions.COW_TABLE_TYPE_OPT_VAL).
     option(HoodieBootstrapConfig.BOOTSTRAP_BASE_PATH_PROP, srcPath).
     option(HoodieBootstrapConfig.BOOTSTRAP_KEYGEN_CLASS, classOf[SimpleKeyGenerator].getName).
     mode(SaveMode.Overwrite).
     save(basePath)

   // Query data after bootstrapping.
   var hoodieROViewDF1 = spark.read.format("hudi").load(basePath + "/*")
   hoodieROViewDF1.show
