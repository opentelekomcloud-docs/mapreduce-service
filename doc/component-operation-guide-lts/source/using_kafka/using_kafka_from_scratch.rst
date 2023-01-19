:original_name: mrs_01_1031.html

.. _mrs_01_1031:

Using Kafka from Scratch
========================

Scenario
--------

You can create, query, and delete topics on a cluster client.

Prerequisites
-------------

The client has been installed. For example, the client is installed in the **/opt/hadoopclient** directory. The client directory in the following operations is only an example. Change it to the actual installation directory.

Using the Kafka Client
----------------------

#. Access the ZooKeeper instance page.

   Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**.

#. View the IP addresses of the ZooKeeper role instance.

   Record any IP address of the ZooKeeper instance.

#. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/hadoopclient/Kafka/kafka/bin**.

   **cd /opt/hadoopclient/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/hadoopclient/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *Kafka user*

#. .. _mrs_01_1031__en-us_topic_0000001219149187_li4808125415465:

   Create a topic.

   **sh kafka-topics.sh --create --topic** *Topic name* **--partitions** *Number of partitions occupied by the topic* **--replication-factor** *Number of replicas of the topic* **--zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

#. Run the following command to view the topic information in the cluster:

   **sh kafka-topics.sh --list --zookeeper** *IP address of the node where the ZooKeeper instance resides\ *\ **:**\ *\ clientPort*\ **/kafka**

#. Delete the topic created in :ref:`7 <mrs_01_1031__en-us_topic_0000001219149187_li4808125415465>`.

   **sh kafka-topics.sh --delete --topic** *Topic name* **--zookeeper** *IP address of the node where the ZooKeeper instance resides*:*clientPort*\ **/kafka**

   Type **y** and press **Enter**.
