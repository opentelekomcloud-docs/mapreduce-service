:original_name: mrs_01_24786.html

.. _mrs_01_24786:

Modifying the Memory Limit of ClickHouse on a ClickHouseServer Node
===================================================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

Modify the maximum memory allowed for ClickHouse on a ClickHouseServer node to ensure the normal use of other service instances on the node.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. Click **Configuration** then **All Configurations**, click **ClickHouseServer(Role)**, and select **Performance**.

   |image1|

#. Change the value of **max_server_memory_usage_to_ram_ratio** as required and save the configuration.

   .. note::

      -  Restart is not required for the modification to take effect.
      -  The value ranges from 0 to 1, indicating the ratio of the total physical RAM of the server that can be used for ClickHouse. For example, if the physical memory of the server is 10 GB and the value of this parameter is **0.9**, the available memory of the ClickHouse service on the current server is 9 GB (10 GB x 0.9). If the value of this parameter is **0**, it indicates that the memory is not limited and the ClickHouse service can use all the physical memory of the server. The value of this parameter can contain a maximum of two decimal places.

.. |image1| image:: /_static/images/en-us_image_0000001583316317.png
