:original_name: mrs_01_2001.html

.. _mrs_01_2001:

Spark Streaming Tuning
======================

Scenario
--------

Streaming is a mini-batch streaming processing framework that features second-level delay and high throughput. To optimize Streaming is to improve its throughput while maintaining second-level delay so that more data can be processed per unit time.

.. note::

   This section applies to the scenario where the input data source is Kafka.

Procedure
---------

A simple streaming processing system consists of a data source, a receiver, and a processor. The data source is Kafka, the receiver is the Kafka data source receiver of Streaming, and the processor is Streaming.

Streaming optimization is to optimize the performance of the three components.

-  **Data source optimization**

   In actual application scenarios, the data source stores the data in the local disks to ensure the error tolerance of the data. However, the calculation results of the Streaming are stored in the memory, and the data source may become the largest bottleneck of the streaming system.

   Kafka can be optimized from the following aspects:

   -  Use Kafka-0.8.2 or later version that allows you to use new Producer APIs in asynchronous mode.
   -  Configure multiple Broker directories, multiple I/O threads, and a proper number of partitions for a topic.

   For details, see section **Performance Tuning** in the Kafka open source documentation at http://kafka.apache.org/documentation.html.

-  **Receiver optimization**

   Streaming has multiple data source receivers, such as Kafka, Flume, MQTT, and ZeroMQ. Kafka has the most receiver types and is the most mature receiver.

   Kafka provides three types of receiver APIs:

   -  KafkaReceiver directly receives Kafka data. If the process is abnormal, data may be lost.
   -  ReliableKafkaReceiver receives data displacement through ZooKeeper records.
   -  DirectKafka reads data from each partition of Kafka through the RDD, ensuring high reliability.

   According to the implementation mechanism and test results, DirectKafka provides better performance than the other two APIs. Therefore, the DirectKafka API is recommended to implement the receiver.

   For details about the Kafka receivers and their optimization methods, see the Kafka open source documentation at http://kafka.apache.org/documentation.html.

-  **Processor optimization**

   The bottom layer of Spark Streaming is executed by Spark. Therefore, most optimization measures for Spark can also be applied to Spark Streaming. The following is an example:

   -  Data serialization
   -  Memory configuration
   -  Configuring DOP
   -  Using the external shuffle service to improve performance

   .. note::

      Higher performance of Spark Streaming indicates lower overall reliability. Examples:

      If **spark.streaming.receiver.writeAheadLog.enable** is set to **false**, disk I/Os are reduced and performance is improved. However, because WAL is disabled, data is lost during fault recovery.

      Therefore, do not disable configuration items that ensure data reliability in production environments during Spark Streaming tuning.

-  **Log archive optimization**

   The **spark.eventLog.group.size** parameter is used to group **JobHistory** logs of an application based on the specified number of jobs. Each group creates a file recording log to prevent **JobHistory** reading failures caused by an oversized log generated during the long-term running of the application. If this parameter is set to **0**, logs are not grouped.

   Most Spark Streaming jobs are small jobs and are generated at a high speed. As a result, frequent grouping is performed and a large number of small log files are generated, consuming disk I/O resources. You are advised to increase the parameter value to, for example, **1000** or greater.
