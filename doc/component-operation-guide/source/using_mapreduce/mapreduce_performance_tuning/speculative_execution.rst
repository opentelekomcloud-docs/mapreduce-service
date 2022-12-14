:original_name: mrs_01_0848.html

.. _mrs_01_0848:

Speculative Execution
=====================

Scenario
--------

If a cluster has hundreds or thousands of nodes, the hardware or software fault of a node may prolong the execution time of the entire task (as most tasks are already completed, the system is still waiting for the task running on the faulty node). Speculative execution allows a task to be executed on multiple machines. You can disable speculative execution for small clusters.

Procedure
---------

Navigation path for setting parameters:

On the **All Configurations** page of the Yarn service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+---------------+
| Parameter                    | Description                                                                                                                             | Default Value |
+==============================+=========================================================================================================================================+===============+
| mapreduce.map.speculative    | Sets whether to execute multiple instances of some map tasks concurrently. **true** indicates that speculative execution is enabled.    | false         |
+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+---------------+
| mapreduce.reduce.speculative | Sets whether to execute multiple instances of some reduce tasks concurrently. **true** indicates that speculative execution is enabled. | false         |
+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+---------------+
