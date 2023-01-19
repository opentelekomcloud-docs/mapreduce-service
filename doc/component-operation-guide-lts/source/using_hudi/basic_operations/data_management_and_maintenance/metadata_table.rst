:original_name: mrs_01_24164.html

.. _mrs_01_24164:

Metadata Table
==============

-  **Introduction**

   A metadata table is a special Hudi metadata table, which is hidden from users. The table stores metadata of a common Hudi table.

   The metadata table is included in a common Hudi table and has a one-to-one mapping relationship with the Hudi table.

-  **Functions**

   Listing massive table partition files in HDFS consumes a large number of RPC requests, reducing HDFS throughput and affecting performance. This problem is more serious for object storage such as OBS. However, a query engine must go through the preceding step before a query.

   Generally, partition information of the current partitioned table is stored in Hive MetaStore. If the partition size of a partitioned table reaches a certain level, the query engine performance deteriorates significantly when querying the partition information of the current table.

-  **Mechanism**

   A metadata table stores the partition information of the current Hudi table and the file information in the partition directory as the metadata information in a special Hudi table. In this way, when a query engine lists partition files of the table, the engine only needs access the metadata table. The RPC pressure of HDFS during query can be greatly reduced with a small volume of metadata information.

   A metadata table is implemented using a Hudi MOR table. Therefore, it can be compacted, cleaned up, and incrementally updated. Unlike similar implementations in other projects, the file listing information is indexed as HFiles, which offers point-lookup performance to obtain partition file listings.

-  **How to Use**

   For Hive query, run **set hoodie.metadata.enable=true**.

   For Spark SQL query, set **--conf spark.hadoop.hoodie.metadata.enable** to **true** when starting Spark SQL.

   When using Spark to write data, set **hoodie.metadata.enable** in the **option** parameter to **true**.

   For details about more parameters, see :ref:`Configuration Reference <mrs_01_24032>` or visit Hudi official website http://hudi.apache.org/docs/configurations.html#metadata-config.

-  **Performance improvement**

   In the test on a large table with 250,000 partition files, the metadata table delivers two to three times speedup over parallelized listing done by Spark.

   .. caution::

      #. .. _mrs_01_24164__en-us_topic_0000001173631260_li1315036193915:

         Do not manually operate a metadata table. Otherwise, data security may be affected.

      #. To use metadata, you must enable metadata for each write operation to ensure data integrity.

      #. When compaction and rollback are performed on tables of Hudi 0.8, data cannot be synchronized to the metadata table.

      #. When metadata is enabled during the clean operation, the metadata table can be updated.

      #. When the number of commits reaches a specified value, compaction, clean, and archive operations are automatically triggered. Therefore, the operation in :ref:`1 <mrs_01_24164__en-us_topic_0000001173631260_li1315036193915>` is unnecessary.
