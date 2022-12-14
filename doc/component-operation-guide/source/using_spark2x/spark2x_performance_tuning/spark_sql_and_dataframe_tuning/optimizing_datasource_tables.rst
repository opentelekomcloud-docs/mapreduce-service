:original_name: mrs_01_1997.html

.. _mrs_01_1997:

Optimizing Datasource Tables
============================

Scenario
--------

Save the partition information about the datasource table to the Metastore and process partition information in the Metastore.

-  Optimize the datasource tables, support syntax such as adding, deletion, and modification in the table based on partitions, improving compatibility with Hive.

-  Support statements of partition tailoring and push down to the Metastore to filter unmatched partitions.

   Example:

   .. code-block::

      select count(*) from table where partCol=1;    //partCol (partition column)

   You need only to process data corresponding to partCol=1 when performing the TableScan operation in the physical plan.

Procedure
---------

If you want to enable Datasource table optimization, configure the **spark-defaults.conf** file on the Spark client.

.. table:: **Table 1** Parameter description

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                       | Description                                                                                                                                                                       | Default Value         |
   +=================================================+===================================================================================================================================================================================+=======================+
   | spark.sql.hive.manageFilesourcePartitions       | Specifies whether to enable Metastore partition management (including datasource tables and converted Hive).                                                                      | true                  |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | -  **true** indicates enabling Metastore partition management. In this case, datasource tables are stored in Hive and Metastore is used to tailor partitions in query statements. |                       |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | -  **false** indicates disabling Metastore partition management.                                                                                                                  |                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.hive.metastorePartitionPruning        | Specifies whether to support pushing down predicate to Hive Metastore.                                                                                                            | true                  |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | -  **true** indicates supporting pushing down predicate to Hive Metastore. Only the predicate of Hive tables is supported.                                                        |                       |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | -  **false** indicates not supporting pushing down predicate to Hive Metastore.                                                                                                   |                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.hive.filesourcePartitionFileCacheSize | The cache size of the partition file metadata in the memory.                                                                                                                      | 250 \* 1024 \* 1024   |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | All tables share a cache that can use up to specified num bytes for file metadata.                                                                                                |                       |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | This parameter is valid only when **spark.sql.hive.manageFilesourcePartitions** is set to **true**.                                                                               |                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.hive.convertMetastoreOrc              | The processing approach of ORC tables.                                                                                                                                            | true                  |
   |                                                 |                                                                                                                                                                                   |                       |
   |                                                 | -  **false**: Spark SQL uses Hive SerDe to process ORC tables.                                                                                                                    |                       |
   |                                                 | -  **true**: Spark SQL uses the Spark built-in mechanism to process ORC tables.                                                                                                   |                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
