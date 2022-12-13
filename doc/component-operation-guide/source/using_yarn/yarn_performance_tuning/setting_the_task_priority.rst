:original_name: mrs_01_0873.html

.. _mrs_01_0873:

Setting the Task Priority
=========================

Scenario
--------

The resource contention scenarios of a cluster are as follows:

#. Submit two jobs (Job 1 and Job 2) with lower priorities.
#. Some tasks of running Job 1 and Job 2 are in the running state. However, some tasks are pending due to resource deficiency because the capacity of cluster or queue resources is limited.
#. Submit a job (Job 3) with a higher priority. In this case, after the running tasks of Job 1 and Job 2 are complete, their resources will be released and then allocated to the pending tasks of Job 3.
#. After Job 3 is complete, its resources will be released and then allocated to Job 1 and Job 2.

Users can use capacity scheduler of ResourceManager to set the task priority in Yarn because the task priority is implemented by the scheduler of ResourceManager.

Procedure
---------

Set the **mapreduce.job.priority** parameter and use CLI or API to set the task priority.

-  Through the CLI

   When submitting tasks, add the **-Dmapreduce.job.priority=**\ *<priority>* parameter.

   *<priority>* can be set to any of the following values:

   -  VERY_HIGH
   -  HIGH
   -  NORMAL
   -  LOW
   -  VERY_LOW

-  Through the API

   You can also set the task priority through the API.

   Set **Configuration.set("mapreduce.job.priority", <priority>)** or **Job.setPriority(JobPriority priority)**.
