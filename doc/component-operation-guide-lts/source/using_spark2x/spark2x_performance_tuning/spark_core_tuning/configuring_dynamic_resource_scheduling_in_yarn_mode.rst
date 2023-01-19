:original_name: mrs_01_1981.html

.. _mrs_01_1981:

Configuring Dynamic Resource Scheduling in Yarn Mode
====================================================

Scenario
--------

Resources are a key factor that affects Spark execution efficiency. When a long-running service (such as the JDBCServer) is allocated with multiple executors without tasks but resources of other applications are insufficient, resources are wasted and scheduled improperly.

Dynamic resource scheduling can add or remove executors of applications in real time based on the task load. In this way, resources are dynamically scheduled to applications.

Procedure
---------

#. Configure the external shuffle service.
#. Log in to FusionInsight Manager, and choose **Cluster** > *Name of the desired cluster* > **Service** > **Spark2x** > **Configuration** > **All Configurations**. Enter **spark.dynamicAllocation.enabled** in the search box and set its value to **true** to enable the dynamic resource scheduling function. This function is disabled by default.

:ref:`Table 1 <mrs_01_1981__en-us_topic_0000001173949934_t55668659f37c4971bbc1bc10ed58a282>` lists some optional configuration items.

.. _mrs_01_1981__en-us_topic_0000001173949934_t55668659f37c4971bbc1bc10ed58a282:

.. table:: **Table 1** Parameters for dynamic resource scheduling

   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | Configuration Item                                       | Description                                                           | Default Value                 |
   +==========================================================+=======================================================================+===============================+
   | spark.dynamicAllocation.minExecutors                     | Indicates the minimum number of executors.                            | 0                             |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.initialExecutors                 | Indicates the number of initial executors.                            | 0                             |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.maxExecutors                     | Indicates the maximum number of executors.                            | 2048                          |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.schedulerBacklogTimeout          | Indicates the first timeout period for scheduling.                    | 1s                            |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.sustainedSchedulerBacklogTimeout | Indicates the second and later timeout interval for scheduling.       | 1s                            |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.executorIdleTimeout              | Indicates the idle timeout interval for common executors.             | 60s                           |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+
   | spark.dynamicAllocation.cachedExecutorIdleTimeout        | Indicates the idle timeout interval for executors with cached blocks. | -  JDBCServer2x: 2147483647s  |
   |                                                          |                                                                       | -  IndexServer2x: 2147483647s |
   |                                                          |                                                                       | -  SparkResource2x: 120       |
   +----------------------------------------------------------+-----------------------------------------------------------------------+-------------------------------+

.. note::

   The external shuffle service must be configured before using the dynamic resource scheduling function.
