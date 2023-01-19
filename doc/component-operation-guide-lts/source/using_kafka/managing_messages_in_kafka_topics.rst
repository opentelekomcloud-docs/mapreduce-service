:original_name: mrs_01_0379.html

.. _mrs_01_0379:

Managing Messages in Kafka Topics
=================================

Scenario
--------

You can produce or consume messages in Kafka topics using the MRS cluster client. For clusters with Kerberos authentication enabled, you must have the permission to perform these operations.

Prerequisites
-------------

You have installed the Kafka client.

Procedure
---------

#. Go to the Kafka service page.

   Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka**.

#. Click **instance**. Query the IP addresses of the Kafka instances.

   Record the IP address of any Kafka instance.

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, /**opt/client/Kafka/kafka/bin**.

   **cd /opt/client/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. For clusters with Kerberos authentication enabled, run the following command to authenticate the user. For clusters with Kerberos authentication disabled, skip this step.

   **kinit** *Kafka user*

   Example:

   **kinit admin**

#. Manage messages in Kafka topics using the following commands:

   -  Producing messages

      **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance resides*\ **:9092 --topic** *Topic name* **--producer.config /opt/client/Kafka/kafka/config/producer.properties**

      You can input specified information as the messages produced by the producer and then press **Enter** to send the messages. To end message producing, press **Ctrl + C** to exit.

   -  Consuming messages

      **sh kafka-console-consumer.sh --topic** *Topic name* **--bootstrap-server** *IP address of the node where the Kafka instance resides*\ **:9092 --consumer.config /opt/client/Kafka/kafka/config/consumer.properties**

      In the configuration file, **group.id** (indicating the consumer group) is set to **example-group1** by default. Users can change the value as required. The value takes effect each time consumption occurs.

      By default, the system reads unprocessed messages in the current consumer group when the command is executed. If a new consumer group is specified in the configuration file and the **--from-beginning** parameter is added to the command, the system reads all messages that have not been automatically deleted in Kafka.

   .. note::

      -  For the IP address of the node where the Kafka instance locates, use the IP address of any broker instance.
      -  If Kerberos authentication is enabled, change the port to **21007**.
      -  By default, the ZooKeeper's **clientPort** value is **2181**.
