:original_name: mrs_01_24035.html

.. _mrs_01_24035:

Batch Write
===========

Scenario
--------

Hudi provides multiple write modes. For details, see the configuration item **hoodie.datasource.write.operation**. This section describes **upsert**, **insert**, and **bulk_insert**.

-  **insert**: The operation process is similar to **upsert**. The query on updated file partitions is not based on indexes. Therefore, **insert** is faster than **upsert**. This operation is recommended for data sources that do not contain updated data. If the data source contains updated data, duplicate data will exist in the data lake.
-  **bulk_insert** (insert in batches): It is used for initial dataset loading. This operation sorts primary keys and then inserts data into a Hudi table by writing data to a common Parquet table. It has the best performance but cannot control small files. The **upsert** and **insert** operations can control small files by using heuristics.
-  **upsert** (insert and update): It is the default operation type. Hudi determines whether historical data exists based on the primary key. Historical data is updated, and other data is inserted. This operation is recommended for data sources, such as change data capture (CDC), that include updated data.

.. note::

   -  Primary keys are not sorted during **insert**. Therefore, you are not advised to use **insert** during dataset initialization.
   -  You are advised to use **insert** if data is new, use **upsert** if data needs to be updated, and use **bulk_insert** if datasets need to be initialized.

Writing Data to Hudi Tables In Batches
--------------------------------------

#. Import the Hudi package to generate test data. For details, see :ref:`2 <mrs_01_24033__li6424125918379>` to :ref:`4 <mrs_01_24033__li654313073616>` in :ref:`Getting Started <mrs_01_24033>`.

#. Add the **option("hoodie.datasource.write.operation", "bulk_insert")** parameter to the command for writing data to a Hudi table to set the write mode to bulk_insert. For example:

   .. code-block::

      df.write.format("org.apache.hudi").
      options(getQuickstartWriteConfigs).
      option("hoodie.datasource.write.precombine.field", "ts").
      option("hoodie.datasource.write.recordkey.field", "uuid").
      option("hoodie.datasource.write.partitionpath.field", "").
      option("hoodie.datasource.write.operation", "bulk_insert").
      option("hoodie.table.name", tableName).
      option("hoodie.datasource.write.keygenerator.class", "org.apache.hudi.keygen.NonpartitionedKeyGenerator").
      option("hoodie.datasource.hive_sync.enable", "true").
      option("hoodie.datasource.hive_sync.partition_fields", "").
      option("hoodie.datasource.hive_sync.partition_extractor_class", "org.apache.hudi.hive.NonPartitionedExtractor").
      option("hoodie.datasource.hive_sync.table", tableName).
      option("hoodie.datasource.hive_sync.use_jdbc", "false").
      option("hoodie.bulkinsert.shuffle.parallelism", 4).
      mode(Overwrite).
      save(basePath)

   .. note::

      -  For details about the parameters in the example, see :ref:`Table 1 <mrs_01_24093__table1815615307121>`.
      -  If the Spark DataSource API is used to update the MOR table, small files of the updated data may be merged when a small volume of data is inserted. As a result, some updated data can be found in the read-optimized view of the MOR table.
      -  If the base file of the data to be updated is a small file, the data to be inserted and new data for update are merged with the base file to generate a new base file instead of being written to logs.

Configuring Partitions
----------------------

Hudi supports multiple partitioning modes, such as multi-level partitioning, non-partitioning, single-level partitioning, and partitioning by date. You can select a proper partitioning mode as required. The following describes how to configure different partitioning modes for Hudi.

-  Multi-level partitioning

   Multi-level partitioning indicates that multiple fields are specified as partition keys. Pay attention to the following configuration items:

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuration Item                                    | Description                                                                                                                                               |
   +=======================================================+===========================================================================================================================================================+
   | hoodie.datasource.write.partitionpath.field           | Configure multiple partition fields, for example, **p1**, **p2**, and **p3**.                                                                             |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_fields          | Set this parameter to **p1**, **p2**, and **p3**. The values must be the same as the partition fields of **hoodie.datasource.write.partitionpath.field**. |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.write.keygenerator.class            | Set this parameter to **org.apache.hudi.keygen.ComplexKeyGenerator**.                                                                                     |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_extractor_class | Set this parameter to **org.apache.hudi.hive.MultiPartKeysValueExtractor**.                                                                               |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Non-partitioning

   Hudi supports non-partitioned tables. Pay attention to the following configuration items:

   +-------------------------------------------------------+------------------------------------------------------------------------------+
   | Configuration Item                                    | Description                                                                  |
   +=======================================================+==============================================================================+
   | hoodie.datasource.write.partitionpath.field           | Leave this parameter blank.                                                  |
   +-------------------------------------------------------+------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_fields          | Leave this parameter blank.                                                  |
   +-------------------------------------------------------+------------------------------------------------------------------------------+
   | hoodie.datasource.write.keygenerator.class            | Set this parameter to **org.apache.hudi.keygen.NonpartitionedKeyGenerator**. |
   +-------------------------------------------------------+------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_extractor_class | Set this parameter to **org.apache.hudi.hive.NonPartitionedExtractor**.      |
   +-------------------------------------------------------+------------------------------------------------------------------------------+

-  Single-level partitioning

   It is similar to multi-level partitioning. Pay attention to the following configuration items:

   +-------------------------------------------------------+--------------------------------------------------------------------------------+
   | Configuration Item                                    | Description                                                                    |
   +=======================================================+================================================================================+
   | hoodie.datasource.write.partitionpath.field           | Set this parameter to one field, for example, **p**.                           |
   +-------------------------------------------------------+--------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_fields          | Set this parameter to **p**.                                                   |
   |                                                       |                                                                                |
   |                                                       | The value must be the same as the partition field of                           |
   |                                                       |                                                                                |
   |                                                       | **hoodie.datasource.write.partitionpath.field**                                |
   +-------------------------------------------------------+--------------------------------------------------------------------------------+
   | hoodie.datasource.write.keygenerator.class            | (Optional) The default value is **org.apache.hudi.keygen.SimpleKeyGenerator**. |
   +-------------------------------------------------------+--------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_extractor_class | Set this parameter to **org.apache.hudi.hive.MultiPartKeysValueExtractor**.    |
   +-------------------------------------------------------+--------------------------------------------------------------------------------+

-  Partitioning by date

   The **date** field is specified as the partition field. Pay attention to the following configuration items:

   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | Configuration Item                                    | Description                                                                                           |
   +=======================================================+=======================================================================================================+
   | hoodie.datasource.write.partitionpath.field           | Set this parameter to the **date** field, for example, **operationTime**.                             |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_fields          | Set this parameter to **operationTime**. The value must be the same as the preceding partition field. |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.write.keygenerator.class            | (Optional) The default value is **org.apache.hudi.keygen.SimpleKeyGenerator**.                        |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | hoodie.datasource.hive_sync.partition_extractor_class | Set this parameter to **org.apache.hudi.hive.SlashEncodedDayPartitionValueExtractor**.                |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------+

   .. note::

      Date format for **SlashEncodedDayPartitionValueExtractor** must be *yyyy/mm/dd*.

-  Partition sorting

   +--------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | Configuration Item                               | Description                                                                                                  |
   +==================================================+==============================================================================================================+
   | hoodie.bulkinsert.user.defined.partitioner.class | Specifies the partition sorting class. You can customize a sorting method. For details, see the sample code. |
   +--------------------------------------------------+--------------------------------------------------------------------------------------------------------------+

   .. note::

      By default, **bulk_insert** sorts data by character and applies only to primary keys of StringType.
