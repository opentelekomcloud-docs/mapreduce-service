:original_name: mrs_01_1578.html

.. _mrs_01_1578:

Pipeline
========

Scenarios
---------

The Netty connection is used among multiple jobs to reduce latency. In this case, NettySink is used on the server and NettySource is used on the client for data transmission.

This section applies to MRS 3.\ *x* or later clusters.

Configuration Description
-------------------------

Configuration items include NettySink information storing path, range of NettySink listening port, whether to enable SSL encryption, domain of the network used for NettySink monitoring.

.. table:: **Table 1** Parameters

   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+----------------------------------------------------------------+
   | Parameter                                   | Description                                                                                                                                                                 | Default Value                                             | Mandatory                                                      |
   +=============================================+=============================================================================================================================================================================+===========================================================+================================================================+
   | nettyconnector.registerserver.topic.storage | Path (on a third-party server) to information about IP address, port numbers, and concurrency of NettySink. ZooKeeper is recommended for storage.                           | /flink/nettyconnector                                     | No. However, if pipeline is enabled, the feature is mandatory. |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+----------------------------------------------------------------+
   | nettyconnector.sinkserver.port.range        | Port range of NettySink.                                                                                                                                                    | If MRS cluster is used, the default value is 28444-28843. | No. However, if pipeline is enabled, the feature is mandatory. |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+----------------------------------------------------------------+
   | nettyconnector.ssl.enabled                  | Whether SSL encryption for the communication between NettySink and NettySource is enabled. For details about the encryption key and protocol, see :ref:`SSL <mrs_01_1569>`. | false                                                     | No. However, if pipeline is enabled, the feature is mandatory. |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+----------------------------------------------------------------+
   | nettyconnector.message.delimiter            | Delimiter used to configure the message sent by NettySink to the NettySource, which is 2-4 bytes long, and cannot contain **\\n**, **#**, or space.                         | The default value is **$\_**.                             | No. However, if pipeline is enabled, the feature is mandatory. |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+----------------------------------------------------------------+
