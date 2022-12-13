:original_name: mrs_01_1075.html

.. _mrs_01_1075:

Service Model Configuration Guide
=================================

This section applies to MRS 3.\ *x* or later.

During Flume service configuration and module selection, the ultimate throughput of a sink must be greater than the maximum throughput of a source. Otherwise, in extreme load scenarios, the write speed of the source to a channel is greater than the read speed of sink from channel. Therefore, the channel is fully occupied due to frequent usage, and the performance is affected.

Avro Source and Avro Sink are usually used in pairs to transfer data between multiple Flume Agents. Therefore, Avro Source and Avro Sink do not become a performance bottleneck in general scenarios.

Inter-Module Performance
------------------------

Based on comparison between the limit performances of modules, Kafka Sink and HDFS Sink can meet the throughput requirements when the front-end is SpoolDir Source. However, HBase Sink could become performance bottlenecks due to the low write performances thereof. As a result, data is stacked in Channel. If you have to use HBase Sink or other sinks that are prone to become performance bottlenecks, you can use **Channel Selector** or **Sink Group** to meet performance requirements.

Channel Selector
----------------

A channel selector allows a source to connect to multiple channels. Data of the source can be distributed or copied by selecting different types of selectors. Currently, a channel selector provided by Flume can be a replicating channel selector or a multiplexing channel selector.

Replicating: indicates that the data of the source is synchronized to all channels.

Multiplexing: indicates that based on the value of a specific field of the header of an event, a channel is selected to send the data. In this way, the data is distributed based on a service type.

-  Replicating configuration example:

   .. code-block::

      client.sources = kafkasource
      client.channels = channel1 channel2
      client.sources.kafkasource.type = org.apache.flume.source.kafka.KafkaSource
      client.sources.kafkasource.kafka.topics = topic1,topic2
      client.sources.kafkasource.kafka.consumer.group.id = flume
      client.sources.kafkasource.kafka.bootstrap.servers = 10.69.112.108:21007
      client.sources.kafkasource.kafka.security.protocol = SASL_PLAINTEXT
      client.sources.kafkasource.batchDurationMillis = 1000
      client.sources.kafkasource.batchSize = 800
      client.sources.kafkasource.channels = channel1 c el2

      client.sources.kafkasource.selector.type = replicating
      client.sources.kafkasource.selector.optional = channel2

   .. table:: **Table 1** Parameters in the Replicating configuration example

      +-------------------+---------------+-------------------------------------------------------+
      | Parameter         | Default Value | Description                                           |
      +===================+===============+=======================================================+
      | Selector.type     | replicating   | Selector type. Set this parameter to **replicating**. |
      +-------------------+---------------+-------------------------------------------------------+
      | Selector.optional | ``-``         | Optional channel. Configure this parameter as a list. |
      +-------------------+---------------+-------------------------------------------------------+

-  Multiplexing configuration example:

   .. code-block::

      client.sources = kafkasource
      client.channels = channel1 channel2
      client.sources.kafkasource.type = org.apache.flume.source.kafka.KafkaSource
      client.sources.kafkasource.kafka.topics = topic1,topic2
      client.sources.kafkasource.kafka.consumer.group.id = flume
      client.sources.kafkasource.kafka.bootstrap.servers = 10.69.112.108:21007
      client.sources.kafkasource.kafka.security.protocol = SASL_PLAINTEXT
      client.sources.kafkasource.batchDurationMillis = 1000
      client.sources.kafkasource.batchSize = 800
      client.sources.kafkasource.channels = channel1 channel2

      client.sources.kafkasource.selector.type = multiplexing
      client.sources.kafkasource.selector.header = myheader
      client.sources.kafkasource.selector.mapping.topic1 = channel1
      client.sources.kafkasource.selector.mapping.topic2 = channel2
      client.sources.kafkasource.selector.default = channel1

   .. table:: **Table 2** Parameters in the Multiplexing configuration example

      +---------------------+-----------------------+--------------------------------------------------------+
      | Parameter           | Default Value         | Description                                            |
      +=====================+=======================+========================================================+
      | Selector.type       | replicating           | Selector type. Set this parameter to **multiplexing**. |
      +---------------------+-----------------------+--------------------------------------------------------+
      | Selector.header     | Flume.selector.header | ``-``                                                  |
      +---------------------+-----------------------+--------------------------------------------------------+
      | Selector.default    | ``-``                 | ``-``                                                  |
      +---------------------+-----------------------+--------------------------------------------------------+
      | Selector.mapping.\* | ``-``                 | ``-``                                                  |
      +---------------------+-----------------------+--------------------------------------------------------+

   In a multiplexing selector example, select a field whose name is topic from the header of the event. When the value of the topic field in the header is topic1, send the event to a channel 1; or when the value of the topic field in the header is topic2, send the event to a channel 2.

   Selectors need to use a specific header of an event in a source to select a channel, and need to select a proper header based on a service scenario to distribute data.

SinkGroup
---------

When the performance of a backend single sink is insufficient, and high reliability or heterogeneous output is required, you can use a sink group to connect a specified channel to multiple sinks, thereby meeting use requirements. Currently, Flume provides two types of sink processors to manage sinks in a sink group. The types are load balancing and failover.

Failover: Indicates that there is only one active sink in the sink group each time, and the other sinks are on standby and inactive. When the active sink becomes faulty, one of the inactive sinks is selected based on priorities to take over services, so as to ensure that data is not lost. This is used in high-reliability scenarios.

Load balancing: Indicates that all sinks in the sink group are active. Each sink obtains data from the channel and processes the data. In addition, during running, loads of all sinks in the sink group are balanced. This is used in performance improvement scenarios.

-  Load balancing configuration examples:

   .. code-block::

      client.sources = source1
      client.sinks = sink1 sink2
      client.channels = channel1

      client.sinkgroups = g1
      client.sinkgroups.g1.sinks = sink1 sink2
      client.sinkgroups.g1.processor.type = load_balance
      client.sinkgroups.g1.processor.backoff = true
      client.sinkgroups.g1.processor.selector = random

      client.sinks.sink1.type = logger
      client.sinks.sink1.channel = channel1

      client.sinks.sink2.type = logger
      client.sinks.sink2.channel = channel1

   .. table:: **Table 3** Parameters of Load Balancing configuration examples

      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                     | Default Value | Description                                                                                                                  |
      +===============================+===============+==============================================================================================================================+
      | sinks                         | ``-``         | Specifies the sink list of the sink group. Multiple sinks are separated by spaces.                                           |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
      | processor.type                | default       | Specifies the type of a processor. Set this parameter to **load_balance**.                                                   |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
      | processor.backoff             | false         | Indicates whether to back off failed sinks exponentially.                                                                    |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
      | processor.selector            | round_robin   | Specifies the selection mechanism. It must be round_robin, random, or a customized class that inherits AbstractSinkSelector. |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
      | processor.selector.maxTimeOut | 30000         | Specifies the time for masking a faulty sink. The default value is 30,000 ms.                                                |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+

-  Failover configuration examples:

   .. code-block::

      client.sources = source1
      client.sinks = sink1 sink2
      client.channels = channel1

      client.sinkgroups = g1
      client.sinkgroups.g1.sinks = sink1 sink2
      client.sinkgroups.g1.processor.type = failover
      client.sinkgroups.g1.processor.priority.sink1 = 10
      client.sinkgroups.g1.processor.priority.sink2 = 5
      client.sinkgroups.g1.processor.maxpenalty = 10000

      client.sinks.sink1.type = logger
      client.sinks.sink1.channel = channel1

      client.sinks.sink2.type = logger
      client.sinks.sink2.channel = channel1

   .. table:: **Table 4** Parameters in the **failover** configuration example

      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                     | Default Value | Description                                                                                                                                                                                                                                                                              |
      +===============================+===============+==========================================================================================================================================================================================================================================================================================+
      | sinks                         | ``-``         | Specifies the sink list of the sink group. Multiple sinks are separated by spaces.                                                                                                                                                                                                       |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | processor.type                | default       | Specifies the type of a processor. Set this parameter to **failover**.                                                                                                                                                                                                                   |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | processor.priority.<sinkName> | ``-``         | Priority. **<sinkName>** must be defined in description of sinks. A sink having a higher priority is activated earlier. A larger value indicates a higher priority. **Note**: If there are multiple sinks, their priorities must be different. Otherwise, only one of them takes effect. |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | processor.maxpenalty          | 30000         | Specifies the maximum backoff time of failed sinks (unit: ms).                                                                                                                                                                                                                           |
      +-------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Interceptors
------------

The Flume interceptor supports modification or discarding of basic unit events during data transmission. You can specify the class name list of built-in interceptors in Flume or develop customized interceptors to modify or discard events. The following table lists the built-in interceptors in Flume. A complex example is used in this section. Other users can configure and use interceptions as required.

.. note::

   1. The interceptor is used between the sources and channels of Flume. Most sources provide parameters for configuring interceptors. You can set the parameters as required.

   2. Flume allows multiple interceptors to be configured for a source. The interceptor names are separated by spaces.

   3. The specified interceptor sequence is the order in which they are called.

   4. The contents inserted by the interceptor in the header can be read and used in sink.

.. table:: **Table 5** Types of built-in interceptors in Flume

   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Interceptor Type               | Description                                                                                                                                                                                        |
   +================================+====================================================================================================================================================================================================+
   | Timestamp Interceptor          | The interceptor inserts a timestamp into the header of an event.                                                                                                                                   |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Host Interceptor               | The interceptor inserts the IP address or host name of the node where the agent is located into the Header of an event.                                                                            |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Remove Header Interceptor      | The interceptor discards the corresponding event based on the strings that matches the regular expression contained in the event header.                                                           |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UUID Interceptor               | The interceptor generates a UUID string for the header of each event.                                                                                                                              |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Search and Replace Interceptor | The interceptor provides a simple string-based search and replacement function based on Java regular expressions. The rule is the same as that of Java Matcher.replaceAll().                       |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Regex Filtering Interceptor    | The interceptor uses the body of an event as a text file and matches the configured regular expression to filter events. The provided regular expression can be used to exclude or include events. |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Regex Extractor Interceptor    | The interceptor extracts content from the original events using a regular expression and adds the content to the header of events.                                                                 |
   +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Regex Filtering Interceptor** is used as an example to describe how to use the interceptor. (For other types of interceptions, see the configuration provided on the official website.)

.. table:: **Table 6** Parameter configuration for **Regex Filtering Interceptor**

   +---------------+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Default Value | Description                                                                                                                                               |
   +===============+===============+===========================================================================================================================================================+
   | type          | ``-``         | Specifies the component type name. The value must be **regex_filter**.                                                                                    |
   +---------------+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | regex         | ``-``         | Specifies the regular expression used to match events.                                                                                                    |
   +---------------+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | excludeEvents | false         | By default, the matched events are collected. If this parameter is set to **true**, the matched events are deleted and the unmatched events are retained. |
   +---------------+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

Configuration example (netcat tcp is used as the source, and logger is used as the sink). After configuring the preceding parameters, run the **telnet** *Host name or IP address* **44444** command on the host where the Linux operating system is run, and enter a string that complies with the regular expression and another does not comply with the regular expression. The log shows that only the matched string is transmitted.

.. code-block::

   #define the source, channel, sink
   server.sources = r1

   server.channels = c1
   server.sinks = k1

   #config the source
   server.sources.r1.type = netcat
   server.sources.r1.bind = ${Host IP address}
   server.sources.r1.port = 44444
   server.sources.r1.interceptors= i1
   server.sources.r1.interceptors.i1.type= regex_filter
   server.sources.r1.interceptors.i1.regex= (flume)|(myflume)
   server.sources.r1.interceptors.i1.excludeEvents= false
   server.sources.r1.channels = c1

   #config the channel
   server.channels.c1.type = memory
   server.channels.c1.capacity = 1000
   server.channels.c1.transactionCapacity = 100
   #config the sink
   server.sinks.k1.type = logger
   server.sinks.k1.channel = c1
