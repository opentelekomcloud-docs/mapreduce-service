:original_name: mrs_01_1700.html

.. _mrs_01_1700:

Why Does Array Border-crossing Occur During FileInputFormat Split?
==================================================================

Question
--------

When HDFS calls the FileInputFormat getSplit method, the ArrayIndexOutOfBoundsException: 0 appears in the following log:

.. code-block::

   java.lang.ArrayIndexOutOfBoundsException: 0
   at org.apache.hadoop.mapred.FileInputFormat.identifyHosts(FileInputFormat.java:708)
   at org.apache.hadoop.mapred.FileInputFormat.getSplitHostsAndCachedHosts(FileInputFormat.java:675)
   at org.apache.hadoop.mapred.FileInputFormat.getSplits(FileInputFormat.java:359)
   at org.apache.spark.rdd.HadoopRDD.getPartitions(HadoopRDD.scala:210)
   at org.apache.spark.rdd.RDD$$anonfun$partitions$2.apply(RDD.scala:239)
   at org.apache.spark.rdd.RDD$$anonfun$partitions$2.apply(RDD.scala:237)
   at scala.Option.getOrElse(Option.scala:120)
   at org.apache.spark.rdd.RDD.partitions(RDD.scala:237)
   at org.apache.spark.rdd.MapPartitionsRDD.getPartitions(MapPartitionsRDD.scala:35)

Answer
------

The elements of each block correspondent frame are as below: /default/rack0/:,/default/rack0/datanodeip:port.

The problem is due to a block damage or loss, making the block correspondent machine ip and port become null. Use **hdfs fsck** to check the file blocks health state when this problem occurs, and remove damaged block or restore the missing block to re-computing the task.
