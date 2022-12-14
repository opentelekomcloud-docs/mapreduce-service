:original_name: mrs_01_0850.html

.. _mrs_01_0850:

Optimizing Performance for Committing MR Jobs
=============================================

Scenario
--------

By default, if an MR job generates a large number of output files, it takes a long time for the job to commit the temporary outputs of a task to the final output directory in the commit phase. In large clusters, the time-consuming commit process of jobs greatly affects the performance.

In this case, you can set the **mapreduce.fileoutputcommitter.algorithm.version** to **2** to improve the performance in the commit phase of MR jobs.

Procedure
---------

Navigation path for setting parameters:

On the **All Configurations** page of the Yarn service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Parameter description

   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                       | Description                                                                                                                                                                                                                         | Default Value         |
   +=================================================+=====================================================================================================================================================================================================================================+=======================+
   | mapreduce.fileoutputcommitter.algorithm.version | Indicates the algorithm version submitted by a job. The value is **1** or **2**.                                                                                                                                                    | 2                     |
   |                                                 |                                                                                                                                                                                                                                     |                       |
   |                                                 | .. note::                                                                                                                                                                                                                           |                       |
   |                                                 |                                                                                                                                                                                                                                     |                       |
   |                                                 |    **2** is the recommended algorithm version. This algorithm enables tasks to directly commit the output results of each task to the final result output directory, reducing the time for the results of large jobs are committed. |                       |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
