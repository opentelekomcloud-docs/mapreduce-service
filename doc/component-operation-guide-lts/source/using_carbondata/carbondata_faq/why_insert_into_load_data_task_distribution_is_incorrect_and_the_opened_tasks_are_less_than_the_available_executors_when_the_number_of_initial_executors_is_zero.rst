:original_name: mrs_01_1464.html

.. _mrs_01_1464:

Why INSERT INTO/LOAD DATA Task Distribution Is Incorrect and the Opened Tasks Are Less Than the Available Executors when the Number of Initial Executors Is Zero?
=================================================================================================================================================================

Question
--------

Why **INSERT INTO or LOAD DATA** task distribution is incorrect, and the openedtasks are less than the available executors when the number of initial executors is zero\ **?**

Answer
------

In case of INSERT INTO or LOAD DATA, CarbonData distributes one task per node. If the executors are not allocated from the distinct nodes then CarbonData will launch fewer tasks.

**Solution**:

Configure higher value for the executor memory and core so that the yarn can launch only one executor per node.

#. Configure the number of the Executor cores.

   -  Configure the **spark.executor.cores** in **spark-defaults.conf** or the **SPARK_EXECUTOR_CORES** in **spark-env.sh** appropriately.
   -  Add **--executor-cores NUM** parameter to configure the cores during use the spark-submit command.

#. Configure the Executor memory.

   -  Configure the **spark.executor.memory** in **spark-defaults.conf** or the **SPARK_EXECUTOR_MEMORY** in **spark-env.sh** appropriately.
   -  Add **--executor-memory MEM** parameter to configure the memory during use the spark-submit command.
