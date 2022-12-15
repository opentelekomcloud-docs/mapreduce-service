:original_name: mrs_01_1570.html

.. _mrs_01_1570:

Network communication (via Netty)
=================================

Scenario
--------

When Flink runs a job, data transmission and reverse pressure detection between tasks depend on Netty. In certain environments, **Netty** parameters should be configured.

Configuration Description
-------------------------

For advanced optimization, you can modify the following Netty configuration items. The default configuration can meet the requirements of tasks of large-scale clusters with high concurrent throughput.

.. table:: **Table 1** Parameter description

   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | Parameter                                          | Description                                                                                                                                                           | Default Value | Mandatory |
   +====================================================+=======================================================================================================================================================================+===============+===========+
   | taskmanager.network.netty.num-arenas               | Number of Netty memory blocks.                                                                                                                                        | 1             | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | taskmanager.network.netty.server.numThreads        | Number of Netty server threads                                                                                                                                        | 1             | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | taskmanager.network.netty.client.numThreads        | Number of Netty client threads                                                                                                                                        | 1             | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | taskmanager.network.netty.client.connectTimeoutSec | Netty client connection timeout duration. Unit: second                                                                                                                | 120           | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | taskmanager.network.netty.sendReceiveBufferSize    | Size of Netty sending and receiving buffers. This defaults to the system buffer size (**cat /proc/sys/net/ipv4/tcp_[rw]mem**) and is 4 MB in modern Linux. Unit: byte | 4096          | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
   | taskmanager.network.netty.transport                | Netty transport type, either **nio** or **epoll**                                                                                                                     | nio           | No        |
   +----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+-----------+
