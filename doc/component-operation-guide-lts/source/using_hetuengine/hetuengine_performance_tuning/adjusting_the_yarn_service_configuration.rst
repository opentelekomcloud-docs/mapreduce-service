:original_name: mrs_01_1740.html

.. _mrs_01_1740:

Adjusting the Yarn Service Configuration
========================================

Scenario
--------

HetuEngine depends on the resource allocation and control capabilities provided by Yarn. You need to adjust the Yarn service configuration based on the actual service and cluster server configuration to achieve the optimal performance.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > **Services** > **Yarn** > **Configurations** > **All Configurations** and set Yarn service parameters by referring to :ref:`Table 1 <mrs_01_1740__en-us_topic_0000001173949262_table49551729155011>`.

   .. _mrs_01_1740__en-us_topic_0000001173949262_table49551729155011:

   .. table:: **Table 1** Yarn configuration parameters

      +------------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                | Default Value | Recommended Value                                                                                                        |
      +==========================================+===============+==========================================================================================================================+
      | yarn.nodemanager.resource.memory-mb      | 16384         | To achieve the optimal performance, set this parameter to 90% of the minimum physical memory of the node in the cluster. |
      +------------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------+
      | yarn.nodemanager.resource.cpu-vcores     | 8             | To achieve the optimal performance, set this parameter to the minimum number of vCores of the node in the cluster.       |
      +------------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------+
      | yarn.scheduler.maximum-allocation-mb     | 65536         | To achieve the optimal performance, set this parameter to 90% of the minimum physical memory of the node in the cluster. |
      +------------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------+
      | yarn.scheduler.maximum-allocation-vcores | 32            | To achieve the optimal performance, set this parameter to the minimum number of vCores of the node in the cluster.       |
      +------------------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------+

#. Click **Save**.

#. Choose **Cluster** > **Services** > **Yarn** > **More** > **Restart Service** to restart the Yarn service for the parameters to take effect.
