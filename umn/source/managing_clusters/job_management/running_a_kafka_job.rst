:original_name: mrs_01_0494.html

.. _mrs_01_0494:

Running a Kafka Job
===================

You can submit programs developed by yourself to MRS to execute them, and obtain the results. This topic describes how to generate and consume messages in a Kafka topic.

Currently, Kafka jobs cannot be submitted on the GUI. You can submit them in the background.

Submitting a Job in the Background
----------------------------------

Query the instance addresses of ZooKeeper and Kafka, and then run the Kafka job.

**Querying the Instance Address** **(3.x)**

#. Log in to the MRS console.
#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.
#. Go to the FusionInsight Manager page. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_0129>`. On MRS Manager, choose **Services** > **ZooKeeper** > **Instance** to query the IP addresses of ZooKeeper instances. Record any IP address of a ZooKeeper instance.
#. Choose **Services** > **Kafka** > **Instance** to query the IP addresses of Kafka instances. Record any IP address of a Kafka instance.

Querying the Instance Address (Versions Earlier Than 3.x)

#. Log in to the MRS console.
#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.
#. On the MRS cluster details page, choose **Components > ZooKeeper > Instance** to query the IP addresses of ZooKeeper instances. Record any IP address of a ZooKeeper instance.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`. Choose **Services** > **ZooKeeper** > **Instance** to query the IP addresses of ZooKeeper instances. Record any IP address of a ZooKeeper instance.

#. Choose **Components > Kafka > Instance** to query the IP addresses of Kafka instances. Record any IP address of a Kafka instance.

**Running a Kafka Job**

In MRS 3.x and later versions, the default installation path of the client is /opt/Bigdata/client. In MRS 3.x and earlier versions, the default installation path is /opt/client. For details, see the actual situation.

#. Log in to the Master2 node. For details, see :ref:`Logging In to an ECS <mrs_01_0083>`.

#. Run the following command to initialize environment variables:

   **source /opt/Bigdata/client/bigdata_env**

#. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If the Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** **MRS cluster user**

   Example: **kinit admin**

#. Run the following command to create a Kafka topic:

   **kafka-topics.sh --create --zookeeper <IP address of the ZooKeeper role instance:2181/kafka> --partitions 2 --replication-factor 2 --topic <Topic name>**

#. Produce messages in a topic test.

   Run the following command: **kafka-console-producer.sh --broker-list <IP address of the Kafka role instance:9092> --topic <Topic name> --producer.config /opt/Bigdata/client/Kafka/kafka/config/producer.properties**.

   Input specified information as the messages produced by the producer and then press **Enter** to send the messages. To end message production, press **Ctrl+C** to exit.

#. Consume messages in the topic test.

   **kafka-console-consumer.sh --topic <Topic name> --bootstrap-server <Kafka role instance IP:210079092> --consumer.config /opt/Bigdata/client/Kafka/kafka/config/consumer.properties**

   .. note::

      If Kerberos authentication is enabled in the cluster, change the port number 9092 to 21007 when running the preceding two commands. For details, see :ref:`List of Open Source Component Ports <mrs_01_0504>`.
