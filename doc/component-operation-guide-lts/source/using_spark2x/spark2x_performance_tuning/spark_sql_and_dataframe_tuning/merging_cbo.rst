:original_name: mrs_01_1998.html

.. _mrs_01_1998:

Merging CBO
===========

Scenario
--------

Spark SQL supports rule-based optimization by default. However, the rule-based optimization cannot ensure that Spark selects the optimal query plan. Cost-Based Optimizer (CBO) is a technology that intelligently selects query plans for SQL statements. After CBO is enabled, the CBO optimizer performs a series of estimations based on the table and column statistics to select the optimal query plan.

Procedure
---------

Perform the following steps to enable CBO:

#. You need to run corresponding SQL commands to collect required table and column statistics.

   SQL commands are as follows (to be chosen as required):

   -  Generate table-level statistics (table scanning):

      **ANALYZE TABLE src COMPUTE STATISTICS**

      This command generates **sizeInBytes** and **rowCount**.

      When you use the ANALYZE statement to collect statistics, sizes of tables not from HDFS cannot be calculated.

   -  Generate table-level statistics (no table scanning):

      **ANALYZE TABLE src COMPUTE STATISTICS NOSCAN**

      This command generates only **sizeInBytes**. Compared with the originally generated **sizeInBytes** and **rowCount** if the **sizeInBytes** remains unchanged, **rowCount** (if any) reserves. Otherwise, **rowCount** is cleared.

   -  Generate column-level statistics:

      **ANALYZE TABLE src COMPUTE STATISTICS FOR COLUMNS a, b, c**

      This command generates column statistics and updates table statistics for consistency. Statistics of complicated data types (such as Seq and Map) and HiveStringType cannot be generated.

   -  Display statistics:

      **DESC FORMATTED src**

      This command displays *xxx* bytes and *xxx* rows in **Statistics** to indicate table-level statistics. You can also run the following command to display column statistics:

      **DESC FORMATTED src a**

   **Limitation**: The current statistics collection does not support statistics for partition levels for partitioned tables.

2. Configure parameters in :ref:`Table 1 <mrs_01_1998__en-us_topic_0000001173790012_t0f01c19bf3d342d69b1e43165d3651c4>` in the **spark-defaults.conf** file on the Spark client.

   .. _mrs_01_1998__en-us_topic_0000001173790012_t0f01c19bf3d342d69b1e43165d3651c4:

   .. table:: **Table 1** Parameter description

      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter                              | Description                                                                                                                    | Default Value         |
      +========================================+================================================================================================================================+=======================+
      | spark.sql.cbo.enabled                  | The switch to enable or disable CBO.                                                                                           | false                 |
      |                                        |                                                                                                                                |                       |
      |                                        | -  **true**: Enable                                                                                                            |                       |
      |                                        | -  **false**: Disable                                                                                                          |                       |
      |                                        |                                                                                                                                |                       |
      |                                        | To enable this function, ensure that statistics of related tables and columns are generated.                                   |                       |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | spark.sql.cbo.joinReorder.enabled      | Specifies whether to automatically adjust the sequence of consecutive inner joins by using CBO.                                | false                 |
      |                                        |                                                                                                                                |                       |
      |                                        | -  **true**: Enable                                                                                                            |                       |
      |                                        | -  **false**: Disable                                                                                                          |                       |
      |                                        |                                                                                                                                |                       |
      |                                        | To enable this function, ensure that statistics of related tables and columns are generated and CBO is enabled.                |                       |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | spark.sql.cbo.joinReorder.dp.threshold | Specifies the threshold of the number of tables that the sequence of consecutive inner joins is automatically adjusted by CBO. | 12                    |
      |                                        |                                                                                                                                |                       |
      |                                        | If the threshold is exceeded, the sequence of joins is not adjusted.                                                           |                       |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------+
