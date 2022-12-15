:original_name: mrs_01_1969.html

.. _mrs_01_1969:

Configuring Local Disk Cache for JobHistory
===========================================

Scenarios
---------

JobHistory can use local disks to cache the historical data of Spark applications to prevent the JobHistory memory from loading a large amount of application data, reducing the memory pressure. In addition, the cached data can be reused to improve the speed for subsequent application access.

Parameter Configuration
-----------------------

Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services **> **Spark2x** > **Configurations**, click the **All Configurations** tab, and search for the following parameters:

+----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| Parameter                        | Description                                                                                                                                                                                             | Default Value                          |
+==================================+=========================================================================================================================================================================================================+========================================+
| spark.history.store.path         | Specifies the local directory for storing historical information for JobHistory. If this parameter is specified, JobHistory caches historical application data in the local disk instead of the memory. | ${BIGDATA_HOME}/tmp/spark2x_JobHistory |
+----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| spark.history.store.maxDiskUsage | Specifies the maximum available space of the local disk cache.                                                                                                                                          | 10 GB                                  |
+----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
