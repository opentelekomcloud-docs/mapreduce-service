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
