:original_name: mrs_01_1966.html

.. _mrs_01_1966:

Hive Dynamic Partition Overwriting Syntax
=========================================

Scenario
--------

In earlier versions, when the **insert overwrite** syntax is used to overwrite partition tables, only partitions with specified expressions are matched, and partitions without specified expressions are deleted. In Spark2.3, partitions without specified expressions are automatically matched. The syntax is the same as that of the dynamic partition matching syntax of Hive.

Parameters
----------

Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations**, click **All Configurations**, and search for the following parameter.

+------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+
| Parameter                                | Description                                                                                                                                                                                                                                                                                                                                                                                       | Default Value | Value Range      |
+==========================================+===================================================================================================================================================================================================================================================================================================================================================================================================+===============+==================+
| spark.sql.sources.partitionOverwriteMode | Specifies the mode for inserting data in partition tables by running the **insert overwrite** command, which can be **STATIC** or **DYNAMIC**. When it is set to **STATIC**, Spark deletes all partitions based on the matching conditions. When it is set to **DYNAMIC**, Spark matches partitions based on matching conditions and dynamically matches partitions without specified conditions. | STATIC        | [STATIC,DYNAMIC] |
+------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+
