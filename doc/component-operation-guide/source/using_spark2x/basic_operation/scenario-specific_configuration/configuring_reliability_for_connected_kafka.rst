:original_name: mrs_01_1960.html

.. _mrs_01_1960:

Configuring Reliability for Connected Kafka
===========================================

Scenario
--------

When the Spark Streaming application is connected to Kafka and the application is restarted, the application reads data from Kafka based on the last read topic offset and the latest offset of the current topic.

If the leader of a Kafka topic fails and the offset of the Kafka leader is greatly different from that of the Kafka follower, the Kafka follower and leader are switched over after the Kafka service is restarted. As a result, the offset of the topic decreases after the Kafka service is restarted.

-  If the Spark Streaming application keeps running, the start position for reading Kafka data is greater than the end position because the offset of the topic in Kafka decreases. As a result, the application cannot read data from Kafka and reports an error.
-  Before restarting the Kafka service, stop the Spark Streaming application. After the Kafka service is restarted, restart the Spark Streaming application to restore the application from the checkpoint. In this case, the Spark Streaming application records the offset position read before the termination and uses the position as the reference to read subsequent data. The Kafka offset decreases (for example, from 100,000 to 10,000). Spark Streaming consumes data only after the offset of the Kafka leader increases to 100,000. As a result, the newly sent data whose offset is between 10,000 and 100,000 is lost.

To resolve the preceding problem, you can configure reliability for Kafka connected to Spark Streaming. After the reliability function of connected Kafka is enabled:

-  If the offset of a topic in Kafka decreases when the Spark Streaming application is running, the latest offset of the topic in Kafka is used as the start position for reading Kafka data and subsequent data is read.

   For a task that has been generated but has not been scheduled, if the read Kafka offset is greater than the latest offset of the topic in Kafka, the task fails to be executed.

   .. note::

      If a large number of tasks fail, the Executor is added to the blacklist. As a result, subsequent tasks cannot be deployed and run. If this happens, you can set **spark.blacklist.enabled** to disable the blacklist function. The blacklist function is enabled by default.

-  If the offset of a topic in Kafka decreases, the Spark Streaming application restarts to restore the unfinished tasks. If the read Kafka offset range is greater than the latest offset of the topic in Kafka, the task is directly discarded.

.. note::

   If the state function is used in the Spark Streaming application, do not enable the reliability function of connected Kafka.

Configuration
-------------

Configure the following parameter in the **spark-defaults.conf** file of the Spark client.

.. table:: **Table 1** Parameter description

   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                         | Description                                                                                  | Default Value         |
   +===================================+==============================================================================================+=======================+
   | spark.streaming.Kafka.reliability | Indicates whether to enable the reliability function for Kafka connected to Spark Streaming. | false                 |
   |                                   |                                                                                              |                       |
   |                                   | -  **true**: The reliability function is enabled.                                            |                       |
   |                                   | -  **false**: The reliability function is disabled.                                          |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
