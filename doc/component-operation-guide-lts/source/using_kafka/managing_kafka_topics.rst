:original_name: mrs_01_0376.html

.. _mrs_01_0376:

Managing Kafka Topics
=====================

Scenario
--------

You can manage Kafka topics on a cluster client based on service requirements. Management permission is required for clusters with Kerberos authentication enabled.

Prerequisites
-------------

You have installed the Kafka client.

Procedure
---------

#. Access the ZooKeeper instance page.

   log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**.

#. View the IP addresses of the ZooKeeper role instance.

   Record any IP address of the ZooKeeper instance.

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, /**opt/client/Kafka/kafka/bin**.

   **cd /opt/client/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to perform user authentication (skip this step in normal mode):

   **kinit** *Component service user*

#. Use **kafka-topics.sh** to manage Kafka topics.

   -  Creating a topic:

      By default, partitions of a topic are distributed based on the number of partitions on the node and disk. To distribute partitions based on the disk capacity, set **log.partition.strategy** to **capacity** for the Kafka service.

      -  **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic*\ **--zookeeper** *IP address of any ZooKeeper node:clientPort*\ **/kafka**
      -  **./kafka-topics.sh --create --topic** *topic name* **--partitions** *number of partitions occupied by the topic*\ **--replication-factor** *number of replicas of the topic* **--bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

   -  List of topics:

      -  **./kafka-topics.sh --list --zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka**
      -  **./kafka-topics.sh --list --bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties**

   -  Viewing the topic:

      -  **./kafka-topics.sh --describe --zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka** --**topic** *topic name*
      -  **./kafka-topics.sh --describe --bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties** **--topic** *topic name*

   -  Modifying a topic:

      -  **./kafka-topics.sh --alter --topic** *topic name*\ **--config** *configuration item=configuration value* **--zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka**

   -  Expanding partitions:

      -  **./kafka-topics.sh --alter --topic** *topic name* **--zookeeper** *service IP address of any ZooKeeper node:clientPort*\ **/kafka --command-config Kafka/kafka/config/client.properties --partitions** *number of partitions after the expansion*
      -  **./kafka-topics.sh --alter --topic** *topic name* **--bootstrap-server** *IP address of the Kafka cluster:21007* **--command-config Kafka/kafka/config/client.properties --partitions** *number of partitions after the expansion*

   -  Deleting a topic

      -  **./kafka-topics.sh --delete --topic** *topic name* **--zookeeper** *Service IP address of any ZooKeeper node:clientPort*\ **/kafka**
      -  **./kafka-topics.sh --delete --topic** *topic name*\ **--bootstrap-server** *IP address of the Kafka cluster:21007* **--command-config ../config/client.properties**
