:original_name: mrs_01_0391.html

.. _mrs_01_0391:

Flume Overview
==============

Flume is a distributed, reliable, and highly available system for aggregating massive logs, which can efficiently collect, aggregate, and move massive log data from different data sources and store the data in a centralized data storage system. Various data senders can be customized in the system to collect data. Additionally, Flume provides simple data processes capabilities and writes data to data receivers (which is customizable).

Flume consists of the client and server, both of which are FlumeAgents. The server corresponds to the FlumeServer instance and is directly deployed in a cluster. The client can be deployed inside or outside the cluster. he client-side and service-side FlumeAgents work independently and provide the same functions.

The client-side FlumeAgent needs to be independently installed. Data can be directly imported to components such as HDFS and Kafka. Additionally, the client-side and service-side FlumeAgents can also work together to provide services.

Process
-------

The process for collecting logs using Flume is as follows:

#. Installing the flume client
#. Configuring the Flume server and client parameters
#. Collecting and querying logs using the Flume client
#. Stopping and uninstalling the Flume client


.. figure:: /_static/images/en-us_image_0000001296060128.png
   :alt: **Figure 1** Log collection process

   **Figure 1** Log collection process

Flume Client
------------

A Flume client consists of the source, channel, and sink. The source sends the data to the channel, and then the sink transmits the data from the channel to the external device. :ref:`Table 1 <mrs_01_0391__en-us_topic_0000001173789528_t3f29550548a749a4831f4ddfc95df002>` describes Flume modules.

.. _mrs_01_0391__en-us_topic_0000001173789528_t3f29550548a749a4831f4ddfc95df002:

.. table:: **Table 1** Module description

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name                              | Description                                                                                                                                                                 |
   +===================================+=============================================================================================================================================================================+
   | Source                            | A source receives or generates data and sends the data to one or multiple channels. The source can work in either data-driven or polling mode.                              |
   |                                   |                                                                                                                                                                             |
   |                                   | Typical sources include:                                                                                                                                                    |
   |                                   |                                                                                                                                                                             |
   |                                   | -  Sources that are integrated with the system and receives data, such as Syslog and Netcat                                                                                 |
   |                                   | -  Sources that automatically generate event data, such as Exec and SEQ                                                                                                     |
   |                                   | -  IPC sources that are used for communication between agents, such as Avro                                                                                                 |
   |                                   |                                                                                                                                                                             |
   |                                   | A Source must associate with at least one channel.                                                                                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Channel                           | A channel is used to buffer data between a source and a sink. After the sink transmits the data to the next channel or the destination, the cache is deleted automatically. |
   |                                   |                                                                                                                                                                             |
   |                                   | The persistency of the channels varies with the channel types:                                                                                                              |
   |                                   |                                                                                                                                                                             |
   |                                   | -  Memory channel: non-persistency                                                                                                                                          |
   |                                   | -  File channel: persistency implemented based on write-ahead logging (WAL)                                                                                                 |
   |                                   | -  JDBC channel: persistency implemented based on the embedded database                                                                                                     |
   |                                   |                                                                                                                                                                             |
   |                                   | Channels support the transaction feature to ensure simple sequential operations. A channel can work with sources and sinks of any quantity.                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Sink                              | Sink is responsible for sending data to the next hop or final destination and removing the data from the channel after successfully sending the data.                       |
   |                                   |                                                                                                                                                                             |
   |                                   | Typical sinks include:                                                                                                                                                      |
   |                                   |                                                                                                                                                                             |
   |                                   | -  Sinks that send storage data to the final destination, such as HDFS and Kafka                                                                                            |
   |                                   | -  Sinks that are consumed automatically, such as Null Sink                                                                                                                 |
   |                                   | -  IPC sinks that are used for communication between agents, such as Avro                                                                                                   |
   |                                   |                                                                                                                                                                             |
   |                                   | A sink must associate with at least one channel.                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

A Flume client can have multiple sources, channels, and sinks. A source can send data to multiple channels, and then multiple sinks send the data out of the client.

Multiple Flume clients can be cascaded. That is, a sink can send data to the source of another client.

Supplementary Information
-------------------------

#. Flume provides the following reliability measures:

   -  The transaction mechanism is implemented between sources and channels, and between channels and sinks.

   -  The sink processor supports the failover and load balancing (load_balance) mechanisms.

      The following is an example of the load balancing (load_balance) configuration:

      .. code-block::

         server.sinkgroups=g1
         server.sinkgroups.g1.sinks=k1 k2
         server.sinkgroups.g1.processor.type=load_balance
         server.sinkgroups.g1.processor.backoff=true
         server.sinkgroups.g1.processor.selector=random

#. The following are precautions for the aggregation and cascading of multiple Flume clients:

   -  Avro or Thrift protocol can be used for cascading.
   -  When the aggregation end contains multiple nodes, evenly distribute the clients to these nodes. Do not connect all the clients to a single node.

#. The Flume client can contain multiple independent data flows. That is, multiple sources, channels, and sinks can be configured in the **properties.properties** configuration file. These components can be linked to form multiple flows.

   For example, to configure two data flows in a configuration, run the following commands:

   .. code-block::

      server.sources = source1 source2
      server.sinks = sink1 sink2
      server.channels = channel1 channel2

      #dataflow1
      server.sources.source1.channels = channel1
      server.sinks.sink1.channel = channel1

      #dataflow2
      server.sources.source2.channels = channel2
      server.sinks.sink2.channel = channel2
