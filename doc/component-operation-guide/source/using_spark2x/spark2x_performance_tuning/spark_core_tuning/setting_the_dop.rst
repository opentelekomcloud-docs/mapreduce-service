:original_name: mrs_01_1978.html

.. _mrs_01_1978:

Setting the DOP
===============

Scenario
--------

The degree of parallelism (DOP) specifies the number of tasks to be executed concurrently. It determines the number of data blocks after the shuffle operation. Configure the DOP to improve the processing capability of the system.

Query the CPU and memory usage. If the tasks and data are not evenly distributed among nodes, increase the DOP. Generally, set the DOP to two or three times that of the total CPUs in the cluster.

Procedure
---------

Configure the DOP parameter using one of the following methods based on the actual memory, CPU, data, and application logic conditions:

-  Configure the DOP parameter in the operation function that generates the shuffle. This method has the highest priority.

   .. code-block::

      testRDD.groupByKey(24)

-  Configure the DOP using **spark.default.parallelism**. This method has the lower priority than the preceding one.

   .. code-block::

      val conf = new SparkConf();
      conf.set("spark.default.parallelism", 24);

-  Configure the value of **spark.default.parallelism** in the **$SPARK_HOME/conf/spark-defaults.conf** file. This method has the lowest priority.

   .. code-block::

      spark.default.parallelism    24
