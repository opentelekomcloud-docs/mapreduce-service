:original_name: mrs_01_1687.html

.. _mrs_01_1687:

Improving Write Performance
===========================

Scenario
--------

Improve the HDFS write performance by modifying the HDFS attributes.

Procedure
---------

Navigation path for setting parameters:

On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations** and select **All Configurations**. Enter a parameter name in the search box.

.. table:: **Table 1** Parameters for improving HDFS write performance

   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                            | Description                                                                                                                                                                                                                                                                                                                           | Default Value         |
   +======================================+=======================================================================================================================================================================================================================================================================================================================================+=======================+
   | dfs.datanode.drop.cache.behind.reads | Specifies whether to enable a DataNode to automatically clear all data in the cache after the data in the cache is transferred to the client.                                                                                                                                                                                         | false                 |
   |                                      |                                                                                                                                                                                                                                                                                                                                       |                       |
   |                                      | If it is set to **true**, the cached data is discarded. The parameter needs to be configured on the DataNode.                                                                                                                                                                                                                         |                       |
   |                                      |                                                                                                                                                                                                                                                                                                                                       |                       |
   |                                      | You are advised to set it to **true** if data is repeatedly read only a few times, so that the cache can be used by other operations. You are advised to set it to **false** if data is repeatedly read many times to enhance the reading speed.                                                                                      |                       |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | dfs.client-write-packet-size         | Specifies the size of the client write packet. When the HDFS client writes data to the DataNode, the data will be accumulated until a packet is generated. Then, the packet is transmitted over the network. This parameter specifies the size (unit: byte) of the data packet to be transmitted, which can be specified by each job. | 262144                |
   |                                      |                                                                                                                                                                                                                                                                                                                                       |                       |
   |                                      | In the 10-Gigabit network, you can increase the value of this parameter to enhance the transmission throughput.                                                                                                                                                                                                                       |                       |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
