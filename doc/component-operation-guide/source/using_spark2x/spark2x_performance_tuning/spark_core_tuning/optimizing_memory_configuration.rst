:original_name: mrs_01_1977.html

.. _mrs_01_1977:

Optimizing Memory Configuration
===============================

Scenario
--------

Spark is a memory-based computing frame. If the memory is insufficient during computing, the Spark execution efficiency will be adversely affected. You can determine whether memory becomes the performance bottleneck by monitoring garbage collection (GC) and evaluating the resilient distributed dataset (RDD) size in the memory, and take performance optimization measures.

To monitor GC of node processes, add the -verbose:gc -XX:+PrintGCDetails -XX:+PrintGCTimeStamps parameter to the **spark.driver.extraJavaOptions** and **spark.executor.extraJavaOptions** in the client configuration file **conf/spark-default.conf**. If "Full GC" is frequently reported, GC needs to be optimized. Cache the RDD and query the RDD size in the log. If a large value is found, change the RDD storage level.

Procedure
---------

-  To optimize GC, adjust the ratio of the young generation and tenured generation. Add **-XX:NewRatio** parameter to the **spark.driver.extraJavaOptions** and **spark.executor.extraJavaOptions** in the client configuration file **conf/spark-default.conf**. For example, export SPARK_JAVA_OPTS=" -XX:NewRatio=2". The new generation accounts for 1/3 of the heap, and the tenured generation accounts for 2/3.

-  Optimize the RDD data structure when compiling Spark programs.

   -  Use primitive arrays to replace fastutil arrays, for example, use fastutil library.
   -  Avoid nested structure.
   -  Avoid using String in keys.

-  Suggest serializing the RDDs when developing Spark programs.

   By default, data is not serialized when RDDs are cached. You can set the storage level to serialize the RDDs and minimize memory usage. For example:

   .. code-block::

      testRDD.persist(StorageLevel.MEMORY_ONLY_SER)
