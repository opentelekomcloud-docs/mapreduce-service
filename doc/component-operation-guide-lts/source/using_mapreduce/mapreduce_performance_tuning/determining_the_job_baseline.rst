:original_name: mrs_01_0845.html

.. _mrs_01_0845:

Determining the Job Baseline
============================

Scenario
--------

The performance optimization effect is verified by comparing actual values with the baseline data. Therefore, determining optimal job baseline is critical to performance optimization.

When determining the job baseline, comply with the following rules:

-  Making full use of cluster resources
-  Setting the number of Map and Reduce tasks appropriately
-  Setting the runtime of each task appropriately

Procedure
---------

-  **Rule 1: Making full use of cluster resources**

   Enable all nodes to handle tasks as actively as they can when a job is executed. Maximizing the number of concurrent tasks helps make full use of resources. You can achieve this purpose by adjusting the data volume to be processed and the number of Map and Reduce tasks.

   You can set **mapreduce.job.reduces** to control the number of Reduce tasks.

   The number of Map tasks depends on the InputFormat type and whether the data file to be processed can be split. By default, TextFileInputFormat allocates Map tasks based on the number of blocks, that is, one Map task for each block. You can adjust the following parameters to improve resource utilization.

   Parameter portal:

   On the **All Configurations** page of the Yarn service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                     | Description                                                                                                                                                                                                                                                                                     | Default Value         |
   +===============================================+=================================================================================================================================================================================================================================================================================================+=======================+
   | mapreduce.input.fileinputformat.split.maxsize | Indicates the maximum size of the data block into which the Map input information is to be split.                                                                                                                                                                                               | ``-``                 |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | The shard size can be calculated based on its size customized by the user and the block size of each file. The formula is as follows:                                                                                                                                                           |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | .. code-block::                                                                                                                                                                                                                                                                                 |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               |    splitSize = Math.max(minSize, Math.min(maxSize, blockSize))                                                                                                                                                                                                                                  |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | If **maxSize** is bigger than **blockSize**, a block is a shard. If **maxSize** is smaller than **blockSize**, a block will be split into multiple shards. If the size of the remaining data in a block is smaller than **splitSize**, the remaining data will be treated as a separated shard. |                       |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | mapreduce.input.fileinputformat.split.minsize | Indicates the minimum size of a data shard.                                                                                                                                                                                                                                                     | 0                     |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

-  **Principle 2: Setting Reduce tasks to be executed in one round.**

   Avoid the following scenarios:

   -  Most of Reduce tasks are completed in the first round, but there is still one Reduce task left running. The execution of the last Reduce task extends the runtime of the job. Therefore, reduce the number of Reduce tasks to enable all of them to run at the same time.
   -  All Map tasks are completed, but there are still Reduce tasks running on some nodes. In this case, the cluster resources are not fully utilized. You need to increase the number of Reduce tasks to enable each node to handle tasks.

-  **Rule 3: Setting the runtime of each task appropriately**

   If each Map or Reduce task of a job takes only a few seconds, most time of the job is wasted on scheduling tasks and starting and stopping processes. Therefore, you need to increase the data volume to be processed in each task. The preferred processing time for each task is 1 minute.

   You can configure the following parameters to adjust the processing time in a task.

   Parameter portal:

   On the **All Configurations** page of the Yarn service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                     | Description                                                                                                                                                                                                                                                                                     | Default Value         |
   +===============================================+=================================================================================================================================================================================================================================================================================================+=======================+
   | mapreduce.input.fileinputformat.split.maxsize | Indicates the maximum size of the data block into which the Map input information is to be split.                                                                                                                                                                                               | ``-``                 |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | The shard size can be calculated based on its size customized by the user and the block size of each file. The formula is as follows:                                                                                                                                                           |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | .. code-block::                                                                                                                                                                                                                                                                                 |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               |    splitSize = Math.max(minSize, Math.min(maxSize, blockSize))                                                                                                                                                                                                                                  |                       |
   |                                               |                                                                                                                                                                                                                                                                                                 |                       |
   |                                               | If **maxSize** is bigger than **blockSize**, a block is a shard. If **maxSize** is smaller than **blockSize**, a block will be split into multiple shards. If the size of the remaining data in a block is smaller than **splitSize**, the remaining data will be treated as a separated shard. |                       |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | mapreduce.input.fileinputformat.split.minsize | Indicates the minimum size of a data shard.                                                                                                                                                                                                                                                     | 0                     |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
