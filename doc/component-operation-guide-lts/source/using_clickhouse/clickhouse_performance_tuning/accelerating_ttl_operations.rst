:original_name: mrs_01_24855.html

.. _mrs_01_24855:

Accelerating TTL Operations
===========================

When TTL is triggered in ClickHouse, a large amount of CPU and memory are consumed.

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. Click **Configurations** then **All Configurations**. Click **ClickHouseServer** > **Customization**, find the **clickhouse-config-customize** parameter, add the following parameters, save the configuration, and restart the service.

+----------------------------------------------------+-----------------------------+----------------------------------------------------------------------------------------------+
| Configuration Item                                 | Reference Value             | Description                                                                                  |
+====================================================+=============================+==============================================================================================+
| merge_tree.max_replicated_merges_with_ttl_in_queue | Half of number of CPU cores | Number of tasks that allow TTL to merge parts concurrently in the ReplicatedMergeTree queue. |
+----------------------------------------------------+-----------------------------+----------------------------------------------------------------------------------------------+
| merge_tree.max_number_of_merges_with_ttl_in_pool   | Number of CPU cores         | The thread pool that allows TTL to merge parts in the ReplicatedMergeTree queue.             |
+----------------------------------------------------+-----------------------------+----------------------------------------------------------------------------------------------+

.. note::

   Do not modify these configurations when the cluster writes heavily. Idle threads need to be reserved for regular Merge operations to avoid the "Too many parts" issue.
