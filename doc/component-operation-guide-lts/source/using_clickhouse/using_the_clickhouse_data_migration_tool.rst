:original_name: mrs_01_24053.html

.. _mrs_01_24053:

Using the ClickHouse Data Migration Tool
========================================

The ClickHouse data migration tool can migrate some partitions of one or more partitioned MergeTree tables on several ClickHouseServer nodes to the same tables on other ClickHouseServer nodes. In the capacity expansion scenario, you can use this tool to migrate data from an original node to a new node to balance data after capacity expansion.

Prerequisites
-------------

-  The ClickHouse and Zookeeper services are running properly. The ClickHouseServer instances on the source and destination nodes are normal.
-  The destination node has the data table to be migrated and the table is a partitioned MergeTree table.
-  Before creating a migration task, ensure that all tasks for writing data to a table to be migrated have been stopped. After the task is started, you can only query the table to be migrated and cannot write data to or delete data from the table. Otherwise, data may be inconsistent before and after the migration.
-  If automatic balancing is enabled, only a partitioned ReplicatedMergeTree table is migrated, and the partitioned table must have a corresponding distributed table.
-  The ClickHouse data directory on the destination node has sufficient space.

Procedure
---------

#. Log in to Manager and choose **Cluster** > **Services** > **ClickHouse** > **Data Migration**. On the displayed page, click **Add Task**.

   .. note::

      -  The number of created migration tasks is limited. By default, a maximum of 20 migration tasks can be created. You can modify the number of migration tasks allowed by modifying the **max_migration_task_number** configuration item on the ClickHouse configuration page of Manager. A migration task occupies a certain number of Znodes on ZooKeeper. Therefore, you are not advised to set the maximum number of migration tasks allowed to a large value.
      -  If the number of existing migration tasks exceeds the upper limit, no more migration tasks can be created. The system automatically deletes the earliest migration tasks that have been successfully executed. If no historical migration task is successfully executed, perform :ref:`10 <mrs_01_24053__en-us_topic_0000001173789598_li246411286161>` based on the site requirements and manually delete historical migration tasks.

2.  On the page for creating a migration task, set the migration task parameters. For details, see :ref:`Table 1 <mrs_01_24053__en-us_topic_0000001173789598_table1724256152117>`. After configuring the parameters, click **Next**. If **Automatic balancing** is not enabled, go to :ref:`3 <mrs_01_24053__en-us_topic_0000001173789598_li117062415510>`. If **Automatic balancing** is enabled, go to :ref:`5 <mrs_01_24053__en-us_topic_0000001173789598_li16513141410554>`.

    .. _mrs_01_24053__en-us_topic_0000001173789598_table1724256152117:

    .. table:: **Table 1** Migration task parameters

       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Parameter                         | Description                                                                                                                                                                                                                                                                    |
       +===================================+================================================================================================================================================================================================================================================================================+
       | Task Name                         | Enter a specific task name. The value can contain 1 to 50 characters, including letters, digits, and underscores (_), and cannot be the same as that of an existing migration task.                                                                                            |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Automatic balancing               | Choose whether to enable **Automatic balancing**.                                                                                                                                                                                                                              |
       |                                   |                                                                                                                                                                                                                                                                                |
       |                                   | -  If it is enabled, the system automatically selects the source and destination nodes to ensure that data in partitioned ReplicatedMergeTree tables corresponding to the distributed tables is evenly distributed on each node in the cluster.                                |
       |                                   | -  If it is not enabled, you need to manually select the source and destination nodes.                                                                                                                                                                                         |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Task Type                         | -  **Scheduled Task**: When the scheduled task is selected, you can set **Started** to specify a time point later than the current time to execute the task.                                                                                                                   |
       |                                   | -  **Immediate task**: The task is executed immediately after it is started.                                                                                                                                                                                                   |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Started                           | Set this parameter when **Task Type** is set to **Scheduled Task**. The valid value is a time point within 90 days from now.                                                                                                                                                   |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Maximum Bandwidth                 | Bandwidth upper limit of each ClickHouseServer node. The value ranges from 1 MB/s to 10,000 MB/s. In automatic balancing scenarios, increase the bandwidth as much as possible. Flow control is disabled by default.                                                           |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
       | Data Amount Migrated              | Percentage of the amount of data migrated in each table to the total amount of data in the table. The value ranges from 0 to 100%. If this parameter is left blank, the value is set to 50% by default. This parameter is valid only when **Automatic balancing** is disabled. |
       +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

3.  .. _mrs_01_24053__en-us_topic_0000001173789598_li117062415510:

    On the **Select Node** page, select the data table to be migrated from the list on the left and click **OK**. In the list on the right, select the source node of the selected data table and click **Next**.

    .. note::

       After a node is selected, other nodes that are replicas of the selected node are automatically selected as the source nodes.

4.  On the **Select Data Table** page, select the host name of the destination node and click **Next**.

    .. note::

       The destination node must be different from the source nodes. The selected source nodes are not displayed on the page.

5.  .. _mrs_01_24053__en-us_topic_0000001173789598_li16513141410554:

    Confirm the task information and click **Submit**.

    The data migration tool automatically calculates the partitions to be migrated based on the size of the data table to be migrated and the value of **Data Amount Migrated** set on the **Add Task** page.

6.  After the migration task is submitted, click **Start** in the **Operation** column. If the task is an immediate task, the task starts to be executed. If the task is a scheduled task, the countdown starts.

7.  During the migration task execution, you can click **Cancel** to cancel the migration task. If the migration task is canceled, the migrated data on the destination node will not be rolled back.

    .. caution::

       After a task with automatic balancing enabled is canceled, it will not stop immediately. It will stop after the table migration is complete. After a task with automatic balancing disabled is canceled, the task stops immediately. After the task stops, a partition may have been migrated to the destination node, but it is not deleted from the source node. In this case, duplicate data exists. Manually check whether the migrated partition still exists on the source node. If it still exists, check that the total data volume of the partition on the destination node is the same as that on the source node, and then delete the partition from the source node.

8.  Choose **More** > **Details** to view details about the migration task.

9.  After the migration is complete, choose **More** > **Results** to view the migration result.

    In a non-automatic balancing task, you can view the migrated partitions of each table and the partition migration result. If the partition migration is not finished, the partition has been copied to the destination node but not deleted from the source node because the data volume of the partition on the source node is inconsistent with that of the partition on the destination node. In this case, check whether the data volume of the partition on the source node is consistent with that of the partition on the destination node, and then delete the partition from the source node.

10. .. _mrs_01_24053__en-us_topic_0000001173789598_li246411286161:

    After the migration is complete, choose **More** > **Delete** to delete the directories related to the migration task on ZooKeeper and the destination node.
