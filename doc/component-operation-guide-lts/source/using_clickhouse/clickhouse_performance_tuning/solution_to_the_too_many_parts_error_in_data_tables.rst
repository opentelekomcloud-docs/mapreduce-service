:original_name: mrs_01_24849.html

.. _mrs_01_24849:

Solution to the "Too many parts" Error in Data Tables
=====================================================

Troubleshooting
---------------

#. Log in to the ClickHouse client and check whether abnormal merge exists.

   **select database, table, elapsed, progress, merge_type from system.merges;**

#. Do not perform the INSERT operation too frequently, do not insert a small amount of data, and increase the interval for inserting data.

#. The data table partitions are not properly allocated. As a result, too many partitions are generated and data tables need to be re-partitioned.

#. If the MERGE operations are not triggered or slow, adjust the following parameters to accelerate them.

   For details, see :ref:`Accelerating Merge Operations <mrs_01_24853>`.

   +----------------------+-------------------------------------------------------------------------------------------------+
   | Configuration Item   | Reference Value                                                                                 |
   +======================+=================================================================================================+
   | max_threads          | Number of CPU cores x 2                                                                         |
   +----------------------+-------------------------------------------------------------------------------------------------+
   | background_pool_size | Number of CPU cores                                                                             |
   +----------------------+-------------------------------------------------------------------------------------------------+
   | merge_max_block_size | The value is an integer multiple of 8192 and is adjusted based on the CPU and memory resources. |
   +----------------------+-------------------------------------------------------------------------------------------------+
   | cleanup_delay_period | Set this parameter to a value that is appropriately less than the default value 30.             |
   +----------------------+-------------------------------------------------------------------------------------------------+

Changing the Value of parts_to_throw_insert
-------------------------------------------

.. caution::

   Increase the value of this parameter only in special scenarios. This configuration acts as a warning for potential issues to some extent. If the cluster hardware resources are insufficient and this configuration is not adjusted properly, potential service issues cannot be detected in a timely manner, which may cause other faults and increase the difficulty of fault recovery.

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. Click **Configurations** then **All Configurations**. Click **ClickHouseServer** > **Customization**, find the **clickhouse-config-customize** parameter, add the following configuration, save it, and restart the service.

+----------------------------------+----------------------------------------------------------------------+
| Name                             | Value                                                                |
+==================================+======================================================================+
| merge_tree.parts_to_throw_insert | Memory of ClickHouse instances/32 GB x 300 (conservative estimation) |
+----------------------------------+----------------------------------------------------------------------+

Verify the modification.

Log in to the ClickHouse client and run the **select \* from system.merge_tree_settings where name = 'parts_to_throw_insert';** command.
