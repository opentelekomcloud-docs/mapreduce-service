:original_name: mrs_01_1982.html

.. _mrs_01_1982:

Configuring Process Parameters
==============================

Scenario
--------

There are three processes in Spark on Yarn mode: driver, ApplicationMaster, and executor. The Driver and Executor handle the scheduling and running of the task. The ApplicationMaster handles the start and stop of the container.

Therefore, the configuration of the driver and executor is very important to run the Spark application. You can optimize the performance of the Spark cluster according to the following procedure.

Procedure
---------

#. Configure the driver memory.

   The driver schedules tasks and communicates with the executor and the ApplicationMaster. Add driver memory when the number and parallelism level of the tasks increases.

   You can configure the driver memory based on the number of the tasks.

   -  Set **spark.driver.memory** in **spark-defaults.conf** to a proper value.
   -  Add the **--driver-memory MEM** parameter to configure the memory when using the **spark-submit** command.

#. Configure the number of the executors.

   One core in an executor can run one task at the same time. Therefore, more tasks can be processed at the same time if you increase the number of the executors. You can add the number of the executors to increase the efficiency if resources are sufficient.

   -  Set **spark.executor.instance** in **spark-defaults.conf** or **SPARK_EXECUTOR_INSTANCES** in **spark-env.sh** to a proper value.
   -  Add the **--num-executors NUM** parameter to configure the number of the executors when using the **spark-submit** command.

#. Configure the number of the executor cores.

   Multiple cores in an executor can run multiple tasks at the same time, which increases the task concurrency. However, because all cores share the memory of an executor, you need to balance the memory and the number of cores.

   -  Set **spark.executor.cores** in **spark-defaults.conf** or **SPARK_EXECUTOR_CORES** in **spark-env.sh** to a proper value.
   -  When you run the **spark-submit** command, add the **--executor-cores NUM** parameter to set the number of executor cores.

#. Configure the executor memory.

   The executor memory is used for task execution and communication. You can increase the memory for a big task that needs more resources, and reduce the memory to increase the concurrency level for a small task that runs fast.

   -  Set **spark.executor.memory** in **spark-defaults.conf** or **SPARK_EXECUTOR_MEMORY** in **spark-env.sh** to a proper value.
   -  When you run the **spark-submit** command, add the **--executor-memory MEM** parameter to set the memory.

Example
-------

-  During the **spark wordcount** calculation, the amount of data is 1.6 TB and the number of the executors is 250.

   The execution fails under the default configuration, and the **Futures timed out** and **OOM** errors occur.

   However each task of wordcount is small and runs fast, the amount of the data is big and the tasks are too many. Therefore the objects on the driver end become huge when there are many tasks. Besides the fact that the executor communicates with the driver once each task is finished, the problem of disconnection between processes caused by insufficient memory occurs.

   The application runs successfully when the memory of the Driver is set to 4 GB.

-  Many errors still occurred in the default configuration when running TPC-DS test on JDBCServer, such as "Executor Lost". When there is 30 GB of driver memory, 2 executor cores, 125 executors, and 6 GB of executor memory, all tasks can be successfully executed.
