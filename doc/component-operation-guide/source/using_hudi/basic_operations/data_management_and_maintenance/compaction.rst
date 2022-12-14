:original_name: mrs_01_24090.html

.. _mrs_01_24090:

Compaction
==========

A compaction merges base and log files of MOR tables.

For MOR tables, data is stored in columnar Parquet files and row-based Avro files, updates are recorded in incremental files, and then a synchronous or asynchronous compaction is performed to generate new versions of columnar files. MOR tables can reduce data ingestion latency, so an asynchronous compaction that does not block ingestion is useful.

An asynchronous compaction is performed in the following two steps:

#. Scheduling a compaction: A compaction is completed by the job of importing data into the data lake. In this step, Hudi scans partitions and selects the file slices to be compacted. A compaction plan is finally written to the Hudi timeline.
#. Executing a compaction: A separate process or thread reads the compaction plan and performs the compaction of file slices.

Compaction can be synchronous or asynchronous.

**Synchronization modes**

-  When HoodieDeltaStreamer is used to write upstream data (Kafka/DFS) to a Hudi dataset, the default value of **--disable-compaction** is **false**, indicating that a compaction is automatically executed.

-  Using DataSource to specify parameters when writing data

   **option("hoodie.compact.inline", "true").**

   **option("hoodie.compact.inline.max.delta.commits", "2").**

**Asynchronous modes**

-  Using Hudi CLI

   Scheduling a compaction:

   **compaction schedule --hoodieConfigs 'hoodie.compaction.strategy=org.apache.hudi.table.action.compact.strategy.BoundedIOCompactionStrategy,hoodie.compaction.target.io=1,hoodie.compact.inline.max.delta.commits=1'**

   Executing a compaction:

   **compaction run --parallelism 100 --sparkMemory 1g --retry 1 --compactionInstant 20210602101315 --hoodieConfigs 'hoodie.compaction.strategy=org.apache.hudi.table.action.compact.strategy.BoundedIOCompactionStrategy,hoodie.compaction.target.io=1,hoodie.compact.inline.max.delta.commits=1' --propsFilePath hdfs://hacluster/tmp/default/tb_test_mor/.hoodie/hoodie.properties --schemaFilePath /tmp/default/tb_test_mor/.hoodie/compact_tb_base.json**

-  Using APIs

   Scheduling a compaction:

   **spark-submit --master yarn --jars /opt/client/Hudi/hudi/lib/hudi-client-common-**\ *xxx*\ **.jar --class org.apache.hudi.utilities.HoodieCompactor /opt/client/Hudi/hudi/lib/hudi-utilities\_**\ *xxx*\ **.jar --base-path /tmp/default/tb_test_mor --table-name tb_test_mor --parallelism 100 --spark-memory 1G --schema-file /tmp/default/tb_test_mor/.hoodie/compact_tb_base.json --instant-time 20210602141810 --schedule --strategy org.apache.hudi.table.action.compact.strategy.UnBoundedCompactionStrategy**

   Executing a compaction:

   **spark-submit --master yarn --jars /opt/client/Hudi/hudi/lib/hudi-client-common-**\ *xxx*\ **.jar --class org.apache.hudi.utilities.HoodieCompactor /opt/client/Hudi/hudi/lib/hudi-utilities\_**\ *xxx*\ **.jar --base-path /tmp/default/tb_test_mor --table-name tb_test_mor --parallelism 100 --spark-memory 1G --schema-file /tmp/default/tb_test_mor/.hoodie/compact_tb_base.json --instant-time 20210602141810**

   .. note::

      -  When using Hudi CLI to schedule a compaction, you do not need to specify **instant-time**, which is automatically generated and returned by the system after the scheduling is successful. You only need to pass this parameter during execution.
      -  For **schema-file**, you need to manually edit the schema file of the current Hudi table and upload it to the server. You can use the schema in the latest **.commit** file.
