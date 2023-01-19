:original_name: mrs_01_1637.html

.. _mrs_01_1637:

Improving Put Performance
=========================

Scenario
--------

In the scenario where a large number of requests are continuously put, setting the following two parameters to **false** can greatly improve the Put performance.

-  **hbase.regionserver.wal.durable.sync**

-  **hbase.regionserver.hfile.durable.sync**

When the performance is improved, there is a low probability that data is lost if three DataNodes are faulty at the same time. Exercise caution when configuring the parameters in scenarios that have high requirements on data reliability.

Procedure
---------

Navigation path for setting parameters:

On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations** > **All Configurations**. Enter the parameter name in the search box, and change the value.

.. table:: **Table 1** Parameters for improving put performance

   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------+
   | Parameter         | Description                                                                                                                                                                                                                         | Value |
   +===================+=====================================================================================================================================================================================================================================+=======+
   | hbase.wal.hsync   | Specifies whether to enable WAL file durability to make the WAL data persistence on disks. If this parameter is set to **true**, the performance is affected because each WAL file is synchronized to the disk by the Hadoop fsync. | false |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------+
   | hbase.hfile.hsync | Specifies whether to enable the HFile durability to make data persistence on disks. If this parameter is set to true, the performance is affected because each Hfile file is synchronized to the disk by the Hadoop fsync.          | false |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------+
