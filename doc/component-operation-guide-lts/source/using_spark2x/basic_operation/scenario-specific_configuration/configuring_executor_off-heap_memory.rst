:original_name: mrs_01_1947.html

.. _mrs_01_1947:

Configuring Executor Off-Heap Memory
====================================

Scenario
--------

When the executor off-heap memory is too small, or processes with higher priority preempt resources, the physical memory usage will exceed the maximal value. To prevent the physical memory usage from exceeding, set the following parameter.

Configuration
-------------

**Navigation path for setting parameters:**

When submitting an application, set the following parameter using **--conf** or adjust the parameter in the **spark-defaults.conf** configuration file on the client.

.. table:: **Table 1** Parameter description

   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                     | Description                                                                                                                                                                                                                                                      | Default Value |
   +===============================+==================================================================================================================================================================================================================================================================+===============+
   | spark.executor.memoryOverhead | Indicates the off-heap memory of each executor, in MB. Increasing the value of this parameter prevents the physical memory usage from exceeding the maximal value. The value is calculated based on max(384, Executor - Memory x 0.1). The minimal value is 384. | 1024          |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
