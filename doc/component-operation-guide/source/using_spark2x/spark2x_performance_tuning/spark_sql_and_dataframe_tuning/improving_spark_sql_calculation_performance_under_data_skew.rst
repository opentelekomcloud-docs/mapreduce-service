:original_name: mrs_01_1987.html

.. _mrs_01_1987:

Improving Spark SQL Calculation Performance Under Data Skew
===========================================================

Scenario
--------

When multiple tables are joined in Spark SQL, skew occurs in join keys and the data volume in some Hash buckets is much higher than that in other buckets. As a result, some tasks with a large amount of data run slowly, resulting low computing performance. Other tasks with a small amount of data are quickly completed, which frees many CPUs and results in a waste of CPU resources.

If the automatic data skew function is enabled, data that exceeds the bucketing threshold is bucketed. Multiple tasks proceed data in one bucket. Therefore, CUP usage is enhanced and the system performance is improved.

.. note::

   Data that has no skew is bucketed and run in the original way.

Restrictions:

-  Only the join between two tables is supported.

-  FULL OUTER JOIN data does not support data skew.

   For example, the following SQL statement indicates that the skew of table **a** or table **b** cannot trigger the optimization.

   **select aid FROM a FULL OUTER JOIN b ON aid=bid;**

-  LEFT OUTER JOIN data does not support the data skew of the right table.

   For example, the following SQL statement indicates that the skew of table **b** cannot trigger the optimization.

   **select aid FROM a LEFT OUTER JOIN b ON aid=bid;**

-  RIGHT OUTER JOIN does not support the data skew of the left table.

   For example, the following SQL statement indicates that the skew of table **a** cannot trigger the optimization.

   **select aid FROM a RIGHT OUTER JOIN b ON aid=bid;**

Configuration Description
-------------------------

Add the following parameters in the following table to the **spark-defaults.conf** configuration file on the Spark driver.

.. table:: **Table 1** Parameter description

   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                                   | Description                                                                                                                                                                                                                                                                                                                                                                                   | Default Value         |
   +=============================================================+===============================================================================================================================================================================================================================================================================================================================================================================================+=======================+
   | spark.sql.adaptive.enabled                                  | The switch to enable the adaptive execution feature.                                                                                                                                                                                                                                                                                                                                          | false                 |
   |                                                             |                                                                                                                                                                                                                                                                                                                                                                                               |                       |
   |                                                             | Note: If AQE and Static Partition Pruning (DPP) are enabled at the same time, DPP takes precedence over AQE during SparkSQL task execution. As a result, AQE does not take effect. The DPP in the cluster is enabled by default. Therefore, you need to disable it when enabling the AQE.                                                                                                     |                       |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.optimizer.dynamicPartitionPruning.enabled         | The switch to enable DPP.                                                                                                                                                                                                                                                                                                                                                                     | true                  |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.adaptive.skewJoin.enabled                         | Specifies whether to enable the function of automatic processing of the data skew in join operations. The function is enabled when this parameter is set to **true** and **spark.sql.adaptive.enabled** is set to **true**.                                                                                                                                                                   | true                  |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.adaptive.skewJoin.skewedPartitionFactor           | This parameter is a multiplier used to determine whether a partition is a data skew partition. If the data size of a partition exceeds the value of this parameter multiplied by the median of the all partition sizes except this partition and exceeds the value of **spark.sql.adaptive.skewJoin.skewedPartitionThresholdInBytes**, this partition is considered as a data skew partition. | 5                     |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.adaptive.skewjoin.skewedPartitionThresholdInBytes | If the partition size (unit: byte) is greater than the threshold as well as the product of the **spark.sql.adaptive.skewJoin.skewedPartitionFactor** value and the median partition size, skew occurs in the partition. Ideally, the value of this parameter should be greater than that of **spark.sql.adaptive.advisoryPartitionSizeInBytes.**.                                             | 256MB                 |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.sql.adaptive.shuffle.targetPostShuffleInputSize       | Minimum amount of shuffle data processed by each task. The unit is byte.                                                                                                                                                                                                                                                                                                                      | 67108864              |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
