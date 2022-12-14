:original_name: mrs_01_1590.html

.. _mrs_01_1590:

Configuring Process Parameters
==============================

Scenario
--------

In Flink on Yarn mode, there are JobManagers and TaskManagers. JobManagers and TaskManagers schedule and run tasks.

Therefore, configuring parameters of JobManagers and TaskManagers can optimize the execution performance of a Flink application. Perform the following steps to optimize the Flink cluster performance.

Procedure
---------

#. Configure JobManager memory.

   JobManagers are responsible for task scheduling and message communications between TaskManagers and ResourceManagers. JobManager memory needs to be increased as the number of tasks and the DOP increases.

   JobManager memory needs to be configured based on the number of tasks.

   -  When running the **yarn-session** command, add the **-jm MEM** parameter to configure the memory.
   -  When running the **yarn-cluster** command, add the **-yjm MEM** parameter to configure the memory.

#. Configure the number of TaskManagers.

   Each core of a TaskManager can run a task at the same time. Increasing the number of TaskManagers has the same effect as increasing the DOP. Therefore, you can increase the number of TaskManagers to improve efficiency when there are sufficient resources.

#. Configure the number of TaskManager slots.

   Multiple cores of a TaskManager can process multiple tasks at the same time. This has the same effect as increasing the DOP. However, the balance between the number of cores and the memory must be maintained, because all cores of a TaskManager share the memory.

   -  When running the **yarn-session** command, add the **-s NUM** parameter to configure the number of slots.
   -  When running the **yarn-cluster** command, add the **-ys NUM** parameter to configure the number of slots.

#. Configure TaskManager memory.

   TaskManager memory is used for task execution and communication. A large-size task requires more resources. In this case, you can increase the memory.

   -  When running the **yarn-session** command, add the **-tm MEM** parameter to configure the memory.
   -  When running the **yarn-cluster** command, add the **-ytm MEM** parameter to configure the memory.
