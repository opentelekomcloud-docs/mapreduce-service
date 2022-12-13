:original_name: mrs_01_1984.html

.. _mrs_01_1984:

Experience
==========

Use mapPartitions to calculate data by partition.
-------------------------------------------------

If the overhead of each record is high, for example:

.. code-block::

   rdd.map{x=>conn=getDBConn;conn.write(x.toString);conn.close}

Use mapPartitions to calculate data by partition.

.. code-block::

   rdd.mapPartitions(records => conn.getDBConn;for(item <- records)
   write(item.toString); conn.close)

Use mapPartitions to flexibly operate data. For example, to calculate the TopN of a large data, mapPartitions can be used to calculate the TopN of each partition and then sort the TopN of all partitions when N is small. Compared with sorting full data for the TopN, this method has the higher efficiency.

Use coalesce to adjust the number of slices.
--------------------------------------------

Use coalesce to adjust the number of slices. There are two coalesce functions:

.. code-block::

   coalesce(numPartitions: Int, shuffle: Boolean = false)

When **shuffle** is set to **true**, the function is the same as repartition(numPartitions:Int). Partitions are recreated using the shuffle. When **shuffle** is set to **false**, partitions of the parent resilient distributed datasets (RDD) are calculated in the same task. In this case, if the value of **numPartitions** is larger than the number of sections of the parent RDD, partitions will not be recreated.

The following scenario is encountered, you can choose the coalesce operator:

-  If the previous operation involves a large number of filters, use coalesce to minimize the number of zero-loaded tasks. In coalesce(numPartitions, false), the value of **numPartitions** is smaller than the number of sections of the parent RDD.
-  Use coalesce when the number of slices entered is too big to execute.
-  Use coalesce when the programs are suspended in the shuffle operation because of a large number of tasks or the Linux resources are limited. In this case, use coalesce(numPartitions, true) to recreate partitions.

Configure a localDir for each disk.
-----------------------------------

During the shuffle procedure of Spark, data needs to be written into local disks. The performance bottleneck of Spark is shuffle, and the bottleneck of shuffle is the I/O. To improve the I/O performance, you can configure multiple disks to implement concurrent data writing. If a node is mounted with multiple disks, configure a Spark local Dir for each disk. This can effectively distribute shuffle files in multiple locations, improving disk I/O efficiency. The performance cannot be improved effectively if a disk is configured with multiple directories.

Collect small data sets.
------------------------

The collect operation does not apply to a large data volume.

When the collect operation is performed, the Executor data will be sent to the Driver. Before performing this operation, ensure that the memory of Driver is sufficient. Otherwise, the Driver process may encounter an OutOfMemory error. If the data volume is unknown, perform the saveAsTextFile operation to write data into the HDFS. If the data volume is known and the Driver has sufficient memory, perform the collect operation.

Use reduceByKey
---------------

reduceByKey causes local aggregation on the Map side, which offers a smooth shuffle procedure. The shuffle operations, like groupByKey, will not perform aggregation on the Map side. Therefore, use reduceByKey as possible as you can, and avoid groupByKey().map(x=>(x._1,x._2.size)).

Broadcast map instead of array.
-------------------------------

If table query is required for each record of the data transmitted from the Driver side, broadcast the data in the set/map instead of Iterator. The query speed of Set/Map is approximately O(1), while the query speed of Iterator is O(n).

Avoid data skew.
----------------

If data skew occurs (certain data volume is extremely large), the execution time of tasks is inconsistent even if there is no Garbage Collection (GC).

-  Redefine the keys. Use keys of smaller granularity to optimize the task size.
-  Modify the degree of parallelism (DOP).

Optimize the data structure.
----------------------------

-  Store data by column. As a result, only the required columns are scanned when data is read.
-  When using the Hash Shuffle, set **spark.shuffle.consolidateFiles** to **true** to combine the intermediate files of shuffle, minimize the number of shuffle files and file I/O operations, and improve performance. The number of final files is the number of reduce tasks.
