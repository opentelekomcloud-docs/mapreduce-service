:original_name: mrs_01_1702.html

.. _mrs_01_1702:

The HDFS Client Is Unresponsive When the NameNode Is Overloaded for a Long Time
===============================================================================

**Question**
------------

When the NameNode node is overloaded (100% of the CPU is occupied), the NameNode is unresponsive. The HDFS clients that are connected to the overloaded NameNode fail to run properly. However, the HDFS clients that are newly connected to the NameNode will be switched to a backup NameNode and run properly.

**Answer**
----------

The default configuration must be used (as described in :ref:`Table 1 <mrs_01_1702__tf99cac42ab7947b3bffe186b74e79d38>`) when the error preceding described occurs: the **keep alive** mechanism is enabled for the RPC connection between the HDFS client and the NameNode. The **keep alive** mechanism will keep the HDFS client waiting for the response from server and prevent the connection from being out timed, causing the unresponsiveness of the HDFS client.

Perform the following operations to the unresponsive HDFS client:

-  Leave the HDFS client waiting. Once the CPU usage of the node where NameNode locates drops, the NameNode will obtain CPU resources and the HDFS client will receive a response.
-  If you do not want to leave the HDFS client running, restart the application where the HDFS client locates to reconnect the HDFS client to another idle NameNode.

Procedure:

Configure the following parameters in the **c**\ **ore-site.xml** file on the client.

.. _mrs_01_1702__tf99cac42ab7947b3bffe186b74e79d38:

.. table:: **Table 1** Parameter description

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                                              | Default Value         |
   +=======================+==========================================================================================================================================================================================================================+=======================+
   | ipc.client.ping       | If the **ipc.client.ping** parameter is configured to **true**, the HDFS client will wait for the response from the server and periodically send the **ping** message to avoid disconnection caused by **tcp timeout**.  | true                  |
   |                       |                                                                                                                                                                                                                          |                       |
   |                       | If the **ipc.client.ping** parameter is configured to **false**, the HDFS client will set the value of **ipc.ping.interval** as the timeout time. If no response is received within that time, timeout occurs.           |                       |
   |                       |                                                                                                                                                                                                                          |                       |
   |                       | To avoid the unresponsiveness of HDFS when the NameNode is overloaded for a long time, you are advised to set the parameter to **false**.                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ipc.ping.interval     | If the value of **ipc.client.ping** is **true**, **ipc.ping.interval** indicates the interval between sending the ping messages.                                                                                         | 60000                 |
   |                       |                                                                                                                                                                                                                          |                       |
   |                       | If the value of **ipc.client.ping** is **false**, **ipc.ping.interval** indicates the timeout time for connection.                                                                                                       |                       |
   |                       |                                                                                                                                                                                                                          |                       |
   |                       | To avoid the unresponsiveness of HDFS when the NameNode is overloaded for a long time, you are advised to set the parameter to a large value, for example **900000** (unit ms) to avoid timeout when the server is busy. |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
