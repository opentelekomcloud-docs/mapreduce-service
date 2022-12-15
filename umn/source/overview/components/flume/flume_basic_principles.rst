:original_name: mrs_08_00161.html

.. _mrs_08_00161:

Flume Basic Principles
======================

`Flume <https://flume.apache.org/>`__ is a distributed, reliable, and HA system that supports massive log collection, aggregation, and transmission. Flume supports customization of various data senders in the log system for data collection. In addition, Flume can roughly process data and write data to various data receivers (customizable). A Flume-NG is a branch of Flume. It is simple, small, and easy to deploy. The following figure shows the basic architecture of the Flume-NG.


.. figure:: /_static/images/en-us_image_0000001296590606.png
   :alt: **Figure 1** Flume-NG architecture

   **Figure 1** Flume-NG architecture

A Flume-NG consists of agents. Each agent consists of three components (source, channel, and sink). A source is used for receiving data. A channel is used for transmitting data. A sink is used for sending data to the next end.

.. table:: **Table 1** Module description

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Module                            | Description                                                                                                                                                                                             |
   +===================================+=========================================================================================================================================================================================================+
   | Source                            | A source receives data or generates data by using a special mechanism, and places the data in batches in one or more channels. The source can work in data-driven or polling mode.                      |
   |                                   |                                                                                                                                                                                                         |
   |                                   | Typical source types are as follows:                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                         |
   |                                   | -  Sources that are integrated with the system, such as Syslog and Netcat                                                                                                                               |
   |                                   | -  Sources that automatically generate events, such as Exec and SEQ                                                                                                                                     |
   |                                   | -  IPC sources that are used for communication between agents, such as Avro                                                                                                                             |
   |                                   |                                                                                                                                                                                                         |
   |                                   | A source must be associated with at least one channel.                                                                                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Channel                           | A channel is used to buffer data between a source and a sink. The channel caches data from the source and deletes that data after the sink sends the data to the next-hop channel or final destination. |
   |                                   |                                                                                                                                                                                                         |
   |                                   | Different channels provide different persistence levels.                                                                                                                                                |
   |                                   |                                                                                                                                                                                                         |
   |                                   | -  Memory channel: non-persistency                                                                                                                                                                      |
   |                                   | -  File channel: Write-Ahead Logging (WAL)-based persistence                                                                                                                                            |
   |                                   | -  JDBC channel: persistency implemented based on the embedded database                                                                                                                                 |
   |                                   |                                                                                                                                                                                                         |
   |                                   | The channel supports the transaction feature to ensure simple sequential operations. A channel can work with sources and sinks of any quantity.                                                         |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Sink                              | A sink sends data to the next-hop channel or final destination. Once completed, the transmitted data is removed from the channel.                                                                       |
   |                                   |                                                                                                                                                                                                         |
   |                                   | Typical sink types are as follows:                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                         |
   |                                   | -  Sinks that send storage data to the final destination, such as HDFS and HBase                                                                                                                        |
   |                                   | -  Sinks that are consumed automatically, such as Null Sink                                                                                                                                             |
   |                                   | -  IPC sinks used for communication between Agents, such as Avro                                                                                                                                        |
   |                                   |                                                                                                                                                                                                         |
   |                                   | A sink must be associated with a specific channel.                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

As shown in :ref:`Figure 2 <mrs_08_00161__fig13368976181048>`, a Flume client can have multiple sources, channels, and sinks.

.. _mrs_08_00161__fig13368976181048:

.. figure:: /_static/images/en-us_image_0000001349390617.png
   :alt: **Figure 2** Flume structure

   **Figure 2** Flume structure

The reliability of Flume depends on transaction switchovers between agents. If the next agent breaks down, the channel stores data persistently and transmits data until the agent recovers. The availability of Flume depends on the built-in load balancing and failover mechanisms. Both the channel and agent can be configured with multiple entities between which they can use load balancing policies. Each agent is a Java Virtual Machine (JVM) process. A server can have multiple agents. Collection nodes (for example, Agents 1, 2, 3) process logs. Aggregation nodes (for example, Agent 4) write the logs into HDFS. The agent of each collection node can select multiple aggregation nodes for load balancing.


.. figure:: /_static/images/en-us_image_0000001296270782.png
   :alt: **Figure 3** Flume cascading

   **Figure 3** Flume cascading

For details about Flume architecture and principles, see https://flume.apache.org/releases/1.9.0.html.

Principle
---------

**Reliability Between Agents**

:ref:`Figure 4 <mrs_08_00161__fig4453710117500>` shows the data exchange between agents.

.. _mrs_08_00161__fig4453710117500:

.. figure:: /_static/images/en-us_image_0000001296430750.png
   :alt: **Figure 4** Data transmission process

   **Figure 4** Data transmission process

#. Flume ensures reliable data transmission based on transactions. When data flows from one agent to another agent, the two transactions take effect. The sink of Agent 1 (agent that sends a message) needs to obtain a message from a channel and sends the message to Agent 2 (agent that receives the message). If Agent 2 receives and successfully processes the message, Agent 1 will submit a transaction, indicating a successful and reliable data transmission.
#. When Agent 2 receives the message sent by Agent 1 and starts a new transaction, after the data is processed successfully (written to a channel), Agent 2 submits the transaction and sends a success response to Agent 1.
#. Before a commit operation, if the data transmission fails, the last transcription starts and retransmits the data that fails to be transmitted last time. The commit operation has written the transaction into a disk. Therefore, the last transaction can continue after the process fails and restores.
