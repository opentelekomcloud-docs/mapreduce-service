:original_name: mrs_01_24485.html

.. _mrs_01_24485:

Closing HDFS Files
==================

Scenario
--------

By default, an HDFS file can be closed only if all blocks are reported (in the **COMPLETED** state). Therefore, the write performance of HDFS is affected by waiting for DataNode blocks and NameNode processing blocks to be reported. For a cluster with heavy load, the waiting consumption has a great impact on the cluster. You can configure the **dfs.namenode.file.close.num-committed-allowed** parameter of HDFS to close files in advance to improve data write performance. However, data may fail to be read because the block cannot be found or the data block information recorded in the NameNode metadata is inconsistent with that stored in the DataNode. Therefore, this feature does not apply to the scenario where data is read immediately after being written. Exercise caution when using this feature.

.. note::

   This section applies to MRS 3.2.0 or later.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **HDFS** and click the **Configurations** tab and then **All Configurations**.
#. Search for and modify the **dfs.namenode.file.close.num-committed-allowed** parameter. For more information, see the following table.

   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                     | Description                                                                                                                                                            |
   +===============================================+========================================================================================================================================================================+
   | dfs.namenode.file.close.num-committed-allowed | Maximum number of blocks in the **COMMITTED** state in the file to be closed.                                                                                          |
   |                                               |                                                                                                                                                                        |
   |                                               | The default value is 0, indicating that this feature is disabled. If this feature is enabled, the recommended value is **1** or **2**.                                 |
   |                                               |                                                                                                                                                                        |
   |                                               | For example, if this parameter is set to **1**, it indicates that a file can be closed without waiting for status of the last block status to change to **COMPLETED**. |
   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Save the configuration.
#. On the **Instance** page of HDFS, select the active and standby NameNode instances, choose **More** > **Instance Rolling Restart**, and wait until the rolling restart is complete.
