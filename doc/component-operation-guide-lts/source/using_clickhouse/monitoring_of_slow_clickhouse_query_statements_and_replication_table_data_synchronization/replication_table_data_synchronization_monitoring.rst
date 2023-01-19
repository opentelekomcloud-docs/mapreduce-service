:original_name: mrs_01_24231.html

.. _mrs_01_24231:

Replication Table Data Synchronization Monitoring
=================================================

Scenario
--------

MRS monitors the synchronization between multiple copies of data in the same shard of a Replicated*MergeTree table.

Constraints
-----------

Currently, you can monitor and query only Replicated*MergeTree tables whose creation statements contain the key word **ON CLUSTER**.

Replication Table Data Synchronization
--------------------------------------

-  **Procedure**

   Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. On the displayed page, click the **Data Synchronization Status** tab.

-  **Data synchronization parameters**

   .. table:: **Table 1** Data synchronization parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                 |
      +===================================+=============================================================================================================================+
      | Data Tables                       | Names of Replicated*MergeTree tables.                                                                                       |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | Shard                             | ClickHouse shard where the data table is located.                                                                           |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | Status                            | Data synchronization status. The options are as follows:                                                                    |
      |                                   |                                                                                                                             |
      |                                   | -  **No data**: The table has no data on this shard.                                                                        |
      |                                   | -  **Synchronized**: The table has data on this shard, and multiple instance copies of the same shard are the same.         |
      |                                   | -  **Not synchronized**: The table has data on this shard, but multiple instance copies of the same shard are not the same. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | Details                           | Data synchronization details of the data table on the corresponding ClickHouseServer instance.                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

-  **Filter conditions**

   You can select **By Data Tables** and enter a data table name in the search box to filter data tables.
