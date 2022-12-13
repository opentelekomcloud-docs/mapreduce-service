:original_name: mrs_01_1962.html

.. _mrs_01_1962:

Filtering Partitions without Paths in Partitioned Tables
========================================================

Scenario
--------

When you perform the **select** query in Hive partitioned tables, the **FileNotFoundException** exception is displayed if a specified partition path does not exist in HDFS. To avoid the preceding exception, configure **spark.sql.hive.verifyPartitionPath** parameter to filter partitions without paths.

Procedure
---------

Perform either of the following methods to filter partitions without paths:

-  Configure the following parameter in the **spark-defaults.conf** file on Spark client.

   .. table:: **Table 1** Parameter description

      +------------------------------------+----------------------------------------------------------------------------------+-----------------------+
      | Parameter                          | Description                                                                      | Default Value         |
      +====================================+==================================================================================+=======================+
      | spark.sql.hive.verifyPartitionPath | Whether to filter partitions without paths when reading Hive partitioned tables. | false                 |
      |                                    |                                                                                  |                       |
      |                                    | **true**: enables the filtering                                                  |                       |
      |                                    |                                                                                  |                       |
      |                                    | **false**: disables the filtering                                                |                       |
      +------------------------------------+----------------------------------------------------------------------------------+-----------------------+

-  When running the spark-submit command to submit an application, configure the **--conf** parameter to filter partitions without paths.

   For example:

   .. code-block::

      spark-submit --class org.apache.spark.examples.SparkPi  --conf spark.sql.hive.verifyPartitionPath=true $SPARK_HOME/lib/spark-examples_*.jar
