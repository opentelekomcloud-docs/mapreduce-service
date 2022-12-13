:original_name: mrs_01_1989.html

.. _mrs_01_1989:

Optimizing the INSERT...SELECT Operation
========================================

Scenario
--------

The INSERT...SELECT operation needs to be optimized if any of the following conditions is true:

-  Many small files need to be queried.
-  A few large files need to be queried.
-  The INSERT...SELECT operation is performed by a non-spark user in Beeline/JDBCServer mode.

Procedure
---------

Optimize the INSERT...SELECT operation as follows:

-  If the table to be created is the Hive table, set the storage type to Parquet. This enables INSERT...SELECT statements to be run faster.
-  Perform the INSERT...SELECT operation as a spark-sql user or spark user (if in Beeline/JDBCServer mode). In this way, it is no longer necessary to change the file owner repeatedly, accelerating the execution of INSERT...SELECT statements.

   .. note::

      In Beeline/JDBCServer mode, the executor user is the same as the driver user. The driver user is a spark user because the driver is a part of JDBCServer service and started by a spark user. If the Beeline user is not a spark user, the file owner must be changed to the Beeline user (actual user) because the executor is unaware of the Beeline user.

-  If many small files need to be queried, set spark.sql.files.maxPartitionBytes and spark.files.openCostInBytes to set the maximum size in bytes of partition and combine multiple small files in a partition to reduce file amount. This accelerates file renaming, ultimately enabling INSERT...SELECT statements to be run faster.

.. note::

   The preceding optimizations are not a one-size-fits-all solution. In the following scenario, it still takes long to perform the INSERT...SELECT operation:

   The dynamic partitioned table contains many partitions.
