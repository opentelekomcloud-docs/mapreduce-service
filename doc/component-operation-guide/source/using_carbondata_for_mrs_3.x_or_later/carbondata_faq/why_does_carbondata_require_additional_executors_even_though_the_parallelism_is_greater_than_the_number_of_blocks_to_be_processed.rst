:original_name: mrs_01_1465.html

.. _mrs_01_1465:

Why Does CarbonData Require Additional Executors Even Though the Parallelism Is Greater Than the Number of Blocks to Be Processed?
==================================================================================================================================

Question
--------

Why does CarbonData require additional executors even though the parallelism is greater than the number of blocks to be processed?

Answer
------

CarbonData block distribution optimizes data processing as follows:

#. Optimize data processing parallelism.
#. Optimize parallel reading of block data.

To optimize parallel processing and parallel read, CarbonData requests executors based on the locality of blocks so that it can obtain executors on all nodes.

If you are using dynamic allocation, you need to configure the following properties:

#. Set **spark.dynamicAllocation.executorIdleTimeout** to 15 minutes (or the average query time).
#. Set **spark.dynamicAllocation.maxExecutors** correctly. The default value **2048** is not recommended. Otherwise, CarbonData will request the maximum number of executors.
#. For a bigger cluster, set **carbon.dynamicAllocation.schedulerTimeout** to a value ranging from 10 to 15 seconds. The default value is 5 seconds.
#. Set **carbon.scheduler.minRegisteredResourcesRatio** to a value ranging from 0.1 to 1.0. The default value is **0.8**. Block distribution can be started as long as the value of **carbon.scheduler.minRegisteredResourcesRatio** is within the range.
