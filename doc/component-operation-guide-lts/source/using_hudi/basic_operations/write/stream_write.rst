:original_name: mrs_01_24036.html

.. _mrs_01_24036:

Stream Write
============

The HoodieDeltaStreamer tool provided by Hudi supports stream write. You can also use SparkStreaming to write data in microbatch mode. HoodieDeltaStreamer provides the following functions:

-  Supports multiple data sources, such as Kafka and DFS.
-  Manages checkpoints, rollback, and recovery to ensure exactly-once semantics.
-  Supports user-defined transformations.

Example:

Prepare the configuration file **kafka-source.properties**.

.. code-block::

   #Hudi configuration
   hoodie.datasource.write.recordkey.field=id
   hoodie.datasource.write.partitionpath.field=age
   hoodie.upsert.shuffle.parallelism=100
   #hive config
   hoodie.datasource.hive_sync.table=hudimor_deltastreamer_partition
   hoodie.datasource.hive_sync.partition_fields=age
   hoodie.datasource.hive_sync.partition_extractor_class=org.apache.hudi.hive.MultiPartKeysValueExtractor
   hoodie.datasource.hive_sync.use_jdbc=false
   hoodie.datasource.hive_sync.support_timestamp=true
   # Kafka Source topic
   hoodie.deltastreamer.source.kafka.topic=hudimor_deltastreamer_partition
   #checkpoint
   hoodie.deltastreamer.checkpoint.provider.path=hdfs://hacluster/tmp/huditest/hudimor_deltastreamer_partition
   # Kafka props
   # The kafka cluster we want to ingest from
   bootstrap.servers= xx.xx.xx.xx:xx
   auto.offset.reset=earliest
   #auto.offset.reset=latest
   group.id=hoodie-delta-streamer
   offset.rang.limit=10000

Run the following commands to specify the HoodieDeltaStreamer execution parameters (for details about the parameter configuration, visit the official website https://hudi.apache.org/ ):

**spark-submit --master yarn**

**--jars /opt/hudi-java-examples-1.0.jar** // Specify the Hudi **jars** directory required for Spark running.

**--driver-memory 1g**

**--executor-memory 1g --executor-cores 1 --num-executors 2 --conf spark.kryoserializer.buffer.max=128m**

**--driver-class-path /opt/client/Hudi/hudi/conf:/opt/client/Hudi/hudi/lib/*:/opt/client/Spark2x/spark/jars/*:/opt/hudi-examples-0.6.1-SNAPSHOT.jar:/opt/hudi-examples-0.6.1-SNAPSHOT-tests.jar** // Specify the Hudi **jars** directory required by the Spark driver.

**--class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer spark-internal**

**--props file:///opt/kafka-source.properties** // Specify the configuration file. You need to set the configuration file path to the HDFS path when submitting tasks in yarn-cluster mode.

**--target-base-path /tmp/huditest/hudimor1_deltastreamer_partition** // Specify the path of the Hudi table.

**--table-type MERGE_ON_READ** // Specify the type of the Hudi table to be written.

**--target-table hudimor_deltastreamer_partition** // Specify the Hudi table name.

**--source-ordering-field name** // Specify the columns to be pre-combined in the Hudi table.

**--source-class org.apache.hudi.utilities.sources.JsonKafkaSource** // Set the consumed data source to **JsonKafkaSource**. Different source classes are specified based on different data sources.

**--schemaprovider-class com.xxxx.bigdata.hudi.examples.DataSchemaProviderExample** // Specify the schema required by the Hudi table.

**--transformer-class com.xxx.bigdata.hudi.examples.TransformerExample** // Specify how to process the data obtained from the data source. Set this parameter based on service requirements.

**--enable-hive-sync** // Enable Hive synchronization to synchronize the Hudi table to Hive.

**--continuous** // Set the stream processing mode to **continuous**.

Stream Write Using HoodieMultiTableDeltaStreamer
------------------------------------------------

.. note::

   HoodieMultiTableDeltaStreamer streaming write applies only to MRS 3.2.0 or later.

HoodieDeltaStreamer allows you to capture data from multiple types of source tables and write the data to Hudi tables. However, you can only write data in one source table to one destination table. By contrast, HoodieMultiTableDeltaStreamer supports data write from multiple source tables to one or multiple destination tables.

-  **The following example describes how to write data in two Kafka source tables to two Hudi tables.**

   .. note::

      Set the following parameters:

      .. code-block::

         // Specify the target table.
         hoodie.deltastreamer.ingestion.tablesToBeIngested=Directory name.target table
         //Specify all source tables to specific destination tables.
         hoodie.deltastreamer.source.sourcesBoundTo.Destination table=Directory name.Source table 1,Directory name.Source table 2
         // Specify the configuration file path of each source table.
         Hoodie.deltastreamer.Source.directory name.Source table 1.configFile=Path 1
         Hoodie.deltastreamer.source.Directory name.Source table 2.configFile=Path 2
         // Specify the check point of each source table. The format of the recovery point varies according to the source table type. For example, the recovery point format of Kafka source is "Topic name,Partition name:offset".
         hoodie.deltastreamer.current.source.checkpoint=Topic name,Partition name:offset
         // Specify the associated table (Hudi table) of each source table. If there are multiple associated tables, separate them with commas (,).
         hoodie.deltastreamer.source.associated.tables=hdfs://hacluster/....., hdfs://hacluster/.....
         // Specify the transform operation before the data in each source table is written to Hudi. Note that the columns to be written must be listed. Do not use select *.
         // <SRC> indicates the current source table and cannot be changed.
         hoodie.deltastreamer.transformer.sql=select field1,field2,field3,... from <SRC>

   Spark submission command:

   .. code-block::

      spark-submit \
      --master yarn \
      --driver-memory 1g \
      --executor-memory 1g \
      --executor-cores 1 \
      --num-executors 5 \
      --conf spark.driver.extraClassPath=/opt/client/Hudi/hudi/conf:/opt/client/Hudi/hudi/lib/*:/opt/client/Spark2x/spark/jars/* \
      --class org.apache.hudi.utilities.deltastreamer.HoodieMultiTableDeltaStreamer /opt/client/Hudi/hudi/lib/hudi-utilities_2.12-*.jar \
      --props file:///opt/hudi/testconf/sourceCommon.properties \
      --config-folder file:///opt/hudi/testconf/ \
      --source-class org.apache.hudi.utilities.sources.JsonKafkaSource \
      --schemaprovider-class org.apache.hudi.examples.common.HoodieMultiTableDeltaStreamerSchemaProvider \
      --transformer-class org.apache.hudi.utilities.transform.SqlQueryBasedTransformer \
      --source-ordering-field col6 \
      --base-path-prefix hdfs://hacluster/tmp/ \
      --table-type COPY_ON_WRITE \
      --target-table KafkaToHudi \
      --enable-hive-sync \
      --allow-fetch-from-multiple-sources \
      --allow-continuous-when-multiple-sources

   .. note::

      #. When the **source** type is **kafka source**, the schema provider class specified by **--schemaprovider-class** needs to be developed by users.
      #. **--allow-fetch-from-multiple-sources** indicates that multi-source table writing is enabled.
      #. **--allow-continuous-when-multiple-sources** indicates that multi-source table continuous write is enabled. If this parameter is not set, the task ends after all source tables are written once.

   sourceCommon.properties:

   .. code-block::

      hoodie.deltastreamer.ingestion.tablesToBeIngested=testdb.KafkaToHudi
      hoodie.deltastreamer.source.sourcesBoundTo.KafkaToHudi=source1,source2
      hoodie.deltastreamer.source.default.source1.configFile=file:///opt/hudi/testconf/source1.properties
      hoodie.deltastreamer.source.default.source2.configFile=file:///opt/hudi/testconf/source2.properties

      hoodie.datasource.write.keygenerator.class=org.apache.hudi.keygen.SimpleKeyGenerator
      hoodie.datasource.write.partitionpath.field=col0
      hoodie.datasource.write.recordkey.field=primary_key
      hoodie.datasource.write.precombine.field=col6

      hoodie.datasource.hive_sync.table=kafkatohudisync
      hoodie.datasource.hive_sync.partition_fields=col0
      hoodie.datasource.hive_sync.partition_extractor_class=org.apache.hudi.hive.MultiPartKeysValueExtractor

      bootstrap.servers=192.168.34.221:21005,192.168.34.136:21005,192.168.34.175:21005
      auto.offset.reset=latest
      group.id=hoodie-test

   source1.properties:

   .. code-block::

      hoodie.deltastreamer.current.source.name=source1 // Specify the name of a Kafka source table.
      hoodie.deltastreamer.source.kafka.topic=s1
      hoodie.deltastreamer.current.source.checkpoint=s1,0:0,1:0 // Checkpoint of the source table when the task is started. The deltastreamer tasks resume from offset 0 of partition 0 and offset 0 of partition 1.
      // Specify the Hudi table to be combined with the source1 table. If the Hudi table has been synchronized to Hive, skip this step and use the table name in the SQL statement.
      hoodie.deltastreamer.source.associated.tables=hdfs://hacluster/tmp/huditest/tb_test_cow_par
      // <SRC> indicates the current source table, that is, source1. The value is fixed.
      hoodie.deltastreamer.transformer.sql=select A.primary_key, A.col0, B.col1, B.col2, A.col3, A.col4, B.col5, B.col6, B.col7 from <SRC> as A join tb_test_cow_par as B on A.primary_key = B.primary_key

   source2.properties

   .. code-block::

      hoodie.deltastreamer.current.source.name=source2
      hoodie.deltastreamer.source.kafka.topic=s2
      hoodie.deltastreamer.current.source.checkpoint=s2,0:0,1:0
      hoodie.deltastreamer.source.associated.tables=hdfs://hacluster/tmp/huditest/tb_test_cow_par
      hoodie.deltastreamer.transformer.sql=select A.primary_key, A.col0, B.col1, B.col2, A.col3, A.col4, B.col5, B.col6, B.col7 from <SRC> as A join tb_test_cow_par as B on A.primary_key = B.primary_key

-  **The following example describes how to write data in two Hudi tables to one Hudi table**

   Spark submission command:

   .. code-block::

      spark-submit \
      --master yarn \
      --driver-memory 1g \
      --executor-memory 1g \
      --executor-cores 1 \
      --num-executors 2 \
      --conf spark.driver.extraClassPath=/opt/client/Hudi/hudi/conf:/opt/client/Hudi/hudi/lib/*:/opt/client/Spark2x/spark/jars/* \
      --class org.apache.hudi.utilities.deltastreamer.HoodieMultiTableDeltaStreamer /opt/client/Hudi/hudi/lib/hudi-utilities_2.12-*.jar \
      --props file:///opt/testconf/sourceCommon.properties \
      --config-folder file:///opt/testconf/ \
      --source-class org.apache.hudi.utilities.sources.HoodieIncrSource \ // Specify that the source table is a Hudi table, which can only be COW.
      --payload-class org.apache.hudi.common.model.OverwriteNonDefaultsWithLatestAvroPayload \ // Specify a payload, which determines how the original value is changed to a new value.
      --transformer-class org.apache.hudi.utilities.transform.SqlQueryBasedTransformer \ // Specify a transformer class. If the schema of the source table is different from that of the target table, the source table data can be written to the target table only after being transformed.
      --source-ordering-field col6 \
      --base-path-prefix hdfs://hacluster/tmp/ \ // Path for saving the destination tables
      --table-type MERGE_ON_READ \ // Type of the destination table, which can be COW or MOR.
      --target-table tb_test_mor_par_300 \ // Specify the name of the target table. When you write data in multiple source tables to a target table, the name of the target table must be specified.
      --checkpoint 000 \ // Specify a checkpoint (commit timestamp), which indicates that Delta Streamer is restored from this checkpoint. 000 indicates that Delta Streamer is restored from the beginning.
      --enable-hive-sync \
      --allow-fetch-from-multiple-sources \
      --allow-continuous-when-multiple-sources \
      --op UPSERT // Specify the write type.

   .. note::

      -  If the **source** type is **HoodieIncrSourc**, **--schemaprovider-class** does not need to be specified.
      -  If **transformer-class** is set to **SqlQueryBasedTransformer**, you can use SQL queries to convert the data structure of the source table to that of the destination table.

   file:///opt/testconf/sourceCommon.properties:

   .. code-block::

      # Common properties of source tables
      hoodie.deltastreamer.ingestion.tablesToBeIngested=testdb.tb_test_mor_par_300 // Specify a target table (common property) to which multiple source tables are written.
      hoodie.deltastreamer.source.sourcesBoundTo.tb_test_mor_par_300=testdb.tb_test_mor_par_100,testdb.tb_test_mor_par_200 //Specify multiple source tables.
      hoodie.deltastreamer.source.testdb.tb_test_mor_par_100.configFile=file:///opt/testconf/tb_test_mor_par_100.properties // Property file path of the source table tb_test_mor_par_100
      hoodie.deltastreamer.source.testdb.tb_test_mor_par_200.configFile=file:///opt/testconf/tb_test_mor_par_200.properties //Property file path of the source table tb_test_mor_par_200

      # Hudi write configurations shared by all source tables. The independent configurations of a source table need to be written to its property file.
      hoodie.datasource.write.keygenerator.class=org.apache.hudi.keygen.SimpleKeyGenerator
      hoodie.datasource.write.partitionpath.field=col0
      hoodie.datasource.write.recordkey.field=primary_key
      hoodie.datasource.write.precombine.field=col6

   file:///opt/testconf/tb_test_mor_par_100.properties

   .. code-block::

      # Configurations of the source table tb_test_mor_par_100
      hoodie.deltastreamer.source.hoodieincr.path=hdfs://hacluster/tmp/testdb/tb_test_mor_par_100 // Path of the source table
      hoodie.deltastreamer.source.hoodieincr.partition.fields=col0 // Partitioning key of the source table
      hoodie.deltastreamer.source.hoodieincr.read_latest_on_missing_ckpt=false
      hoodie.deltastreamer.source.associated.tables=hdfs://hacluster/tmp/testdb/tb_test_mor_par_400 //Specify the table to be associated with the source table.
      hoodie.deltastreamer.transformer.sql=select A.primary_key, A.col0, B.col1, B.col2, A.col3, A.col4, B.col5, A.col6, B.col7 from <SRC> as A join tb_test_mor_par_400 as B on A.primary_key = B.primary_key //This configuration takes effect only when transformer-class is set to SqlQueryBasedTransformer.

   file:///opt/testconf/tb_test_mor_par_200.properties

   .. code-block::

      # Configurations of the source table tb_test_mor_par_200
      hoodie.deltastreamer.source.hoodieincr.path=hdfs://hacluster/tmp/testdb/tb_test_mor_par_200
      hoodie.deltastreamer.source.hoodieincr.partition.fields=col0
      hoodie.deltastreamer.source.hoodieincr.read_latest_on_missing_ckpt=false
      hoodie.deltastreamer.source.associated.tables=hdfs://hacluster/tmp/testdb/tb_test_mor_par_400
      hoodie.deltastreamer.transformer.sql=select A.primary_key, A.col0, B.col1, B.col2, A.col3, A.col4, B.col5, A.col6, B.col7 from <SRC> as A join tb_test_mor_par_400 as B on A.primary_key = B.primary_key //Convert the data structure of the source table to that of the destination table. If the source table needs to be associated with Hive, you can use the table name in the SQL query for association. If the source table needs to be associated with a Hudi table, you need to specify the path of the Hudi table first and then use the table name in the SQL query for association.
