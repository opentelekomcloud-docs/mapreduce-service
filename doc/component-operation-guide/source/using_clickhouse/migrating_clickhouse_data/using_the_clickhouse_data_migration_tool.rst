:original_name: mrs_01_24198.html

.. _mrs_01_24198:

Using the ClickHouse Data Migration Tool
========================================

The ClickHouse data migration tool can migrate some partitions of one or more partitioned MergeTree tables on several ClickHouseServer nodes to the same tables on other ClickHouseServer nodes. In the capacity expansion scenario, you can use this tool to migrate data from an original node to a new node to balance data after capacity expansion.

Prerequisites
-------------

-  The ClickHouse and Zookeeper services are running properly. The ClickHouseServer instances on the source and destination nodes are normal.
-  The destination node has the data table to be migrated and the table is a partitioned MergeTree table.
-  Before creating a migration task, ensure that all tasks for writing data to a table to be migrated have been stopped. After the task is started, you can only query the table to be migrated and cannot write data to or delete data from the table. Otherwise, data may be inconsistent before and after the migration.
-  The ClickHouse data directory on the destination node has sufficient space.

Procedure
---------

#. Log in to Manager and choose **Cluster** > **Services** > **ClickHouse**. On the ClickHouse service page, click the **Data Migration** tab.
#. Click **Add Task**.

3. On the page for creating a migration task, set the migration task parameters. For details, see :ref:`Table 1 <mrs_01_24198__table1724256152117>`.

   .. _mrs_01_24198__table1724256152117:

   .. table:: **Table 1** Migration task parameters

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                         |
      +===================================+=====================================================================================================================================================================================+
      | Task Name                         | Enter a specific task name. The value can contain 1 to 50 characters, including letters, arrays, and underscores (_), and cannot be the same as that of an existing migration task. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Type                         | -  **Scheduled Task**: When the scheduled task is selected, you can set **Started** to specify a time point later than the current time to execute the task.                        |
      |                                   | -  **Immediate task**: The task is executed immediately after it is started.                                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Started                           | Set this parameter when **Task Type** is set to **Scheduled Task**. The valid value is a time point within 90 days from now.                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

4. On the **Select Node** page, specify **Source Node Host Name** and **Destination Node Host Name**, and click **Next**.

   .. note::

      -  Only one host name can be entered in **Source Node Host Name** and **Destination Node Host Name**, respectively. Multi-node migration is not supported.

         To obtain the parameter values, click the **Instance** tab on the ClickHouse service page and view the **Host Name** column of the current ClickHouseServer instance.

      -  **Maximum Bandwidth** is optional. If it is not specified, there is no upper limit. The maximum bandwidth can be set to **10000** MB/s.

5. On the **Select Data Table** page, click |image1| next to **Database**, select the database to be migrated on the source node, and select the data table to be migrated for **Data Table**. The data table drop-down list displays the partitioned MergeTree tables in the selected database. In the **Node Information** area, the space usage of the ClickHouse service data directory on the current source and destination nodes is displayed. Click **Next**.

6. Confirm the task information and click **Submit**.

   The data migration tool automatically calculates the partitions to be migrated based on the size of the data table. The amount of data to be migrated is the total size of the partitions to be migrated.

7. After the migration task is submitted, click **Start** in the **Operation** column. If the task is an immediate task, the task starts to be executed. If the task is a scheduled task, the countdown starts.

8. During the migration task execution, you can click **Cancel** to cancel the migration task that is being executed. If you cancel the task, the migrated data on the destination node will be rolled back.

   You can choose **More** > **Details** to view the log information during the migration.

9. After the migration is complete, choose **More** > **Results** to view the migration result and choose **More** > **Delete** to delete the directories related to the migration task on ZooKeeper and the source node.

.. |image1| image:: /_static/images/en-us_image_0000001349170269.png
