:original_name: mrs_01_0849.html

.. _mrs_01_0849:

Using Slow Start
================

Scenario
--------

The Slow Start feature specifies the proportion of Map tasks to be completed before Reduce tasks are started. If the Reduce tasks are started too early, resources will be occupied, thereby reducing task running efficiency. However, if the Reduce tasks are started at an appropriate time, resource usage during shuffle and task running efficiency will be improved. For example, the MapReduce job includes 15 Map tasks and a cluster can start 10 Map tasks, there are 5 Map tasks remained after a round of Map tasks is completed and the cluster has available resources. In this case, you can configure the value of Slow Start to a value less than 1 (for example, 0.8), then the Reduce tasks can make use of the remaining cluster resources.

Procedure
---------

Parameter portal:

On the **All Configurations** page of the MapReduce service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| Parameter                                    | Description                                                                                                                                                                            | Default Value |
+==============================================+========================================================================================================================================================================================+===============+
| mapreduce.job.reduce.slowstart.completedmaps | Fraction of the number of Maps in the job which should be completed before Reduces are scheduled for the job. By default, the Reduce tasks start when all the Map tasks are completed. | 1.0           |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
