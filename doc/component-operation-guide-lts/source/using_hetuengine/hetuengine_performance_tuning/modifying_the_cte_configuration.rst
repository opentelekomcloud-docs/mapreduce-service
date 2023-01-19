:original_name: mrs_01_24181.html

.. _mrs_01_24181:

Modifying the CTE Configuration
===============================

Scenario
--------

If a table or common table expression (CTE) contained in a query appears multiple times and has the same projection and filter, you can enable the CTE reuse function to cache data in memory. In this way, you do not need to read data from disks for multiple times, reducing the time required for query execution.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations** and configure related parameters by referring to :ref:`Table 1 <mrs_01_24181__en-us_topic_0000001219231083_table1201657173018>`.

   .. _mrs_01_24181__en-us_topic_0000001219231083_table1201657173018:

   .. table:: **Table 1** CTE configuration parameters

      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------+--------------------------------------------------------------------+
      | Parameter                             | Description                                                                                                                                                           | Recommended Value | Default Value | Parameter File                                                     |
      +=======================================+=======================================================================================================================================================================+===================+===============+====================================================================+
      | optimizer.reuse-table-scan            | Whether to enable the CTE table data reuse function.                                                                                                                  | true              | false         | **coordinator.config.properties** and **worker.config.properties** |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------+--------------------------------------------------------------------+
      | experimental.spill-reuse-tablescan    | Whether to enable the function of spilling memory to disks during tablescan reuse.                                                                                    | true              | false         | **coordinator.config.properties** and **worker.config.properties** |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------+--------------------------------------------------------------------+
      | optimizer.cte-reuse-enabled           | Whether to enable CTE reuse. If this function is enabled, CTE is executed only once irrespective of the number of times the same CTE is being used in the main query. | true              | false         | **coordinator.config.properties** and **worker.config.properties** |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------+--------------------------------------------------------------------+
      | dynamic-filtering-max-per-driver-size | Maximum volume of data that can be collected by each driver when dynamic filtering starts.                                                                            | 100MB             | 1MB           | **coordinator.config.properties** and **worker.config.properties** |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+---------------+--------------------------------------------------------------------+

#. Click **Save**.

#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Restart Service** and enter the password to restart the HetuEngine service for the parameters to take effect.
