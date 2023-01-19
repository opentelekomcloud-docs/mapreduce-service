:original_name: mrs_01_0861.html

.. _mrs_01_0861:

Configure the ApplicationMaster to Automatically Adjust the Allocated Memory
============================================================================

Scenario
--------

During the process of starting the configuration, when the ApplicationMaster creates a container, the allocated memory is automatically adjusted according to the total number of tasks, which makes resource utilization more flexible and improves the fault tolerance of the client application.

Configuration Description
-------------------------

**Navigation path for setting parameters:**

On Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **Yarn** > **Configuration**. On the displayed page, select **All Configurations** and enter **mapreduce.job.am.memory.policy**.

**Configuration description**

If the default value of the parameter is left empty. In this case, the automatic adjustment policy is not enabled. The memory of ApplicationMaster is still affected by the value of **yarn.app.mapreduce.am.resource.mb**.

The value of **mapreduce.job.am.memory.policy** consists of five items, and they are separated by colons (:) and commas (,) in the following format: **baseTaskCount:taskStep:memoryStep,minMemory:maxMemory**. The format is strictly checked when the value is entered.

.. table:: **Table 1** Parameter description

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter             | Description                                                                                                                                                                                                                                | Setting Requirement                                                                                         |
   +=======================+============================================================================================================================================================================================================================================+=============================================================================================================+
   | baseTaskCount         | Indicates the total number of tasks. The configuration of ApplicationMaster is valid only when the total number of tasks (on the sum of the Map and Reduce ends) is greater than or equal to the value of this parameter.                  | The value cannot be empty and must be greater than 0.                                                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | taskStep              | Indicates the incremental step length of tasks. This parameter and **memoryStep** determine the memory adjustment amount.                                                                                                                  | The value cannot be empty and must be greater than 0.                                                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | memoryStep            | Indicates the incremental memory step. The memory capacity is increased based on the value of **yarn.app.mapreduce.am.resource.mb**.                                                                                                       | The value cannot be empty and must be greater than 0. The unit is MB.                                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | minMemory             | Indicates the lower limit of the memory that can be automatically adjusted. If the memory after the automatic adjustment is less than or equal to the value of this parameter, the value of **yarn.app.mapreduce.am.resource.mb** is used. | The value cannot be empty. It must be greater than 0 and cannot be greater than the value of **maxMemory**. |
   |                       |                                                                                                                                                                                                                                            |                                                                                                             |
   |                       |                                                                                                                                                                                                                                            | Unit: MB                                                                                                    |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | maxMemory             | Indicates the upper limit of memory that can ve automatically adjusted. If the adjusted memory exceeds the upper limit, use this value as the final value.                                                                                 | The value cannot be empty. It must be greater than 0 and cannot be less than the value of **minMemory**.    |
   |                       |                                                                                                                                                                                                                                            |                                                                                                             |
   |                       |                                                                                                                                                                                                                                            | Unit: MB                                                                                                    |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+

Example Value
-------------

Configuration:

-  yarn.app.mapreduce.am.resource.mb=1536
-  mapreduce.job.am.memory.policy=100:10:50,1200:2000
-  Total number of tasks of an application =120

The calculation process is as follows:

Memory after adjustment = 1536 + [(120 - 100)/10] x 50 = 1636. In this example, memory after adjustment 1636 is greater than the value of **minMemory** **1200**, and less than the value of **maxMemory** **2000**. Therefore, the ApplicationMaster memory is set to **1636 MB**.

If the value of **memStep** is changed to **250**, the calculation formula is as follows: Memory after adjustment = 1536 + [(120 - 100) / 10] x 250 = 2136. In this case, the memory after adjustment is greater than the value of **maxMemory** **2000**. As a result, the value of **ApplicationMaster** is set to **2000 MB**.

.. note::

   If the memory after adjustment is lower than the value of **minMemory**, the configuration does not take effect but the value is still printed on the backend server. This value is provided as the reference for adjusting the value of **minMemory**.
