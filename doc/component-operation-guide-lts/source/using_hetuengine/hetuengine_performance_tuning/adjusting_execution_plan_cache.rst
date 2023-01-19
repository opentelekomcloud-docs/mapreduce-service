:original_name: mrs_01_1742.html

.. _mrs_01_1742:

Adjusting Execution Plan Cache
==============================

Scenario
--------

HetuEngine provides the execution plan cache function. For the same query that needs to be executed for multiple times, this function reduces the time required for generating the execution plans for the same query.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations** and adjust the execution plan cache parameters by referring to :ref:`Table 1 <mrs_01_1742__en-us_topic_0000001219350551_table0600139102317>`.

   .. _mrs_01_1742__en-us_topic_0000001219350551_table0600139102317:

   .. table:: **Table 1** Execution plan cache parameters

      +----------------------------------+---------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
      | Parameter                        | Default Value | Recommended Value                                   | Description                                                                                         | Parameter File                                                     |
      +==================================+===============+=====================================================+=====================================================================================================+====================================================================+
      | hetu.executionplan.cache.enabled | false         | true                                                | Indicates whether to enable the global execution plan cache.                                        | **coordinator.config.properties** and **worker.config.properties** |
      +----------------------------------+---------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
      | hetu.executionplan.cache.limit   | 20000         | Adjust the value based on application requirements. | Indicates the maximum number of execution plans that can be cached.                                 | **coordinator.config.properties** and **worker.config.properties** |
      +----------------------------------+---------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
      | hetu.executionplan.cache.timeout | 86400000      | Adjust the value based on application requirements. | Indicates the timeout interval of the cached execution plan since the last access, in milliseconds. | **coordinator.config.properties** and **worker.config.properties** |
      +----------------------------------+---------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+

#. Click **Save**.

#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Restart Service** to restart the HetuEngine service for the parameters to take effect.
