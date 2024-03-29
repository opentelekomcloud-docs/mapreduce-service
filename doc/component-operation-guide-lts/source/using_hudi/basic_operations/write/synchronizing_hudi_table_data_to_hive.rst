:original_name: mrs_01_24064.html

.. _mrs_01_24064:

Synchronizing Hudi Table Data to Hive
=====================================

You can run **run_hive_sync_tool.sh** to synchronize data in the Hudi table to Hive.

For example, run the following command to synchronize the Hudi table in the **hdfs://hacluster/tmp/huditest/hudimor1_deltastreamer_partition** directory on HDFS to the Hive table **table hive_sync_test3** with **unite**, **country**, and **state** as partition keys:

.. code-block::

   run_hive_sync_tool.sh --partitioned-by unite,country,state --base-path hdfs://hacluster/tmp/huditest/hudimor1_deltastreamer_partition --table hive_sync_test3 --partition-value-extractor org.apache.hudi.hive.MultiPartKeysValueExtractor --support-timestamp

.. table:: **Table 1** Parameter description

   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | Command                          | Description                                                                                                                                                                                                      | Mandatory or Not (Yes or No) | Default Value                          |
   +==================================+==================================================================================================================================================================================================================+==============================+========================================+
   | --database                       | Specifies the Hive database name.                                                                                                                                                                                | No                           | default                                |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --table                          | Specifies the Hive table name.                                                                                                                                                                                   | Yes                          | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --base-file-format               | Specifies the file format (**PARQUET** or **HFILE**).                                                                                                                                                            | No                           | PARQUET                                |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --user                           | Specifies the Hive username.                                                                                                                                                                                     | No                           | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --pass                           | Specifies the Hive password.                                                                                                                                                                                     | No                           | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --jdbc-url                       | Specifies the Hive JDBC connection URL.                                                                                                                                                                          | No                           | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --base-path                      | Specifies the storage path of the Hudi table to be synchronized.                                                                                                                                                 | Yes                          | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --partitioned-by                 | Specifies the partition key.                                                                                                                                                                                     | No                           | ``-``                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --partition-value-extractor      | Specifies the partition class. PartitionValueExtractor needs to be implemented. The partition value can be extracted from the HDFS path.                                                                         | No                           | SlashEncodedDayPartitionValueExtractor |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --assume-date-partitioning       | Creates partitions in yyyy/mm/dd format to support backward compatibility.                                                                                                                                       | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --use-pre-apache-input-format    | Use InputFormat in the **com.uber.hoodie** package to replace the one in the **org.apache.hudi** package. Do not use this command except for migrating projects from **com.uber.hoodie** to **org.apache.hudi**. | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --use-jdbc                       | Uses Hive JDBC connection.                                                                                                                                                                                       | No                           | true                                   |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --auto-create-database           | Specifies whether to automatically create a Hive database.                                                                                                                                                       | No                           | true                                   |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --skip-ro-suffix                 | Specifies whether to skip the read-optimized view with the **\_ro** suffix during registration.                                                                                                                  | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --use-file-listing-from-metadata | Specifies whether to obtain the file list from the Hudi metadata.                                                                                                                                                | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --verify-metadata-file-listing   | Specifies whether to verify the file list in the Hudi metadata based on the file system.                                                                                                                         | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --help/-h                        | Specifies whether to display help information.                                                                                                                                                                   | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --support-timestamp              | Specifies whether to convert **TIMESTAMP_MICROS** of INT64 to Hive timestamp.                                                                                                                                    | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --decode-partition               | Specifies whether to decode the partition value if the partition is encoded during the write process.                                                                                                            | No                           | false                                  |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+
   | --batch-sync-num                 | Specifies the number of Hive partitions to be synchronized in each batch.                                                                                                                                        | No                           | 1000                                   |
   +----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+----------------------------------------+

.. note::

   During Hive synchronization, if the table does not exist, an external table is created and partitions are added. If the table exists, check whether table schemas are different. If they are different, replace the table. Check whether new partitions exist. If new partitions exist, partitions are added accordingly.

   Therefore, there are the following restrictions when Hive synchronization is used:

   -  Fields can only be added to the schema and cannot be modified or deleted.
   -  Partition directories can only be added but cannot be deleted.
   -  **Overwrite** can only overwrite the Hudi table. The Hive table cannot be overwritten synchronously.
   -  Do not use the timestamp type as the partition column when synchronizing a Hudi table to Hive.
   -  When this script is used for synchronization, JDBC must be used for security purposes. That is, **--use-jdbc** must be set to **true**.
