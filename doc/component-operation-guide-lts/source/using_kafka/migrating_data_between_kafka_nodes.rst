:original_name: mrs_01_24534.html

.. _mrs_01_24534:

Migrating Data Between Kafka Nodes
==================================

This section applies to MRS 3.2.0 or later.

Scenario
--------

This section describes how to use Kafka client commands to migrate partition data between disks on a node without stopping the Kafka service.

Prerequisites
-------------

-  The MRS cluster administrator has understood service requirements and prepared a Kafka user (belonging to the **kafkaadmin** group. It is not required for the normal mode.).
-  The Kafka client has been installed.
-  The Kafka instance status and disk status are normal.
-  Based on the current disk space usage of the partition to be migrated, ensure that the disk space will be sufficient after the migration.

Procedure
---------

#. Log in as a client installation user to the node on which the Kafka client is installed.

#. Run the following command to switch to the Kafka client installation directory, for example, **/opt/kafkaclient**:

   **cd /opt/kafkaclient**

#. Run the following command to set environment variables:

   **source bigdata_env**

#. Run the following command to authenticate the user (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to switch to the Kafka client directory:

   **cd Kafka/kafka/bin**

#. .. _mrs_01_24534__li420725319552:

   Run the following command to view the topic details of the partition to be migrated:

   **Security mode:**

   **./kafka-topics.sh --describe --bootstrap-server** *IP address of the Kafkacluster:21007* **--command-config ../config/client.properties** **--topic** *topic name*

   **Normal mode:**

   **./kafka-topics.sh --describe --bootstrap-server** *IP address of the Kafka cluster:21005* **--command-config ../config/client.properties** **--topic** *Topic name*

   |image1|

#. .. _mrs_01_24534__li1824951465613:

   Run the following command to query the mapping between **Broker_ID** and the IP address:

   **./kafka-broker-info.sh --zookeeper** *IP address of the ZooKeeper quorumpeer instance*:*ZooKeeper port number*\ **/kafka**

   .. code-block::

      Broker_ID     IP_Address
      --------------------------
      4           192.168.0.100
      5           192.168.0.101
      6           192.168.0.102

   .. note::

      -  IP address of the ZooKeeper quorumpeer instance

         To obtain IP addresses of all ZooKeeper quorumpeer instances, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Instance** and view the IP addresses of all the hosts where the quorumpeer instances locate.

      -  Port number of the ZooKeeper client

         Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the displayed page, click **Configurations** and check the value of **clientPort**. The default value is **24002**.

#. .. _mrs_01_24534__li1230081019282:

   Obtain the partition distribution and node information from the command output in :ref:`6 <mrs_01_24534__li420725319552>` and :ref:`7 <mrs_01_24534__li1824951465613>`, and create the JSON file for reallocation in the current directory.

   To migrate data in the partition whose **Broker_ID** is **6** to the **/srv/BigData/hadoop/data1/kafka-logs** directory, the required JSON configuration file is as follows:

   .. code-block::

      {"partitions":[{"topic": "testws","partition": 2,"replicas": [6,5],"log_dirs": ["/srv/BigData/hadoop/data1/kafka-logs","any"]}],"version":1}

   .. note::

      -  **topic** indicates the topic name, for example, **testws**.
      -  **partition** indicates the topic partition.
      -  The number in **replicas** corresponds to **Broker_ID**.
      -  **log_dirs** indicates the path of the disk to be migrated. In this example, **log_dirs** of the node whose **Broker_ID** is **5** is set to **any**, and that of the node whose **Broker_ID** is **6** is set to **/srv/BigData/hadoop/data1/kafka-logs.** Note that the path must correspond to the node.

#. Run the following command to perform reallocation:

   **Security mode:**

   **./kafka-reassign-partitions.sh** **--bootstrap-server** *Service IP address of Broker*\ **:21007** **--command-config ../config/client.properties** **--zookeeper** *{zk_host}:{port}*\ **/kafka** **--reassignment-json-file** *Path of the JSON file compiled in :ref:`8 <mrs_01_24534__li1230081019282>`* **--execute**

   **Normal mode:**

   **./kafka-reassign-partitions.sh** **--bootstrap-server** *Service IP address of Broker*\ **:21005** **--command-config ../config/client.properties** **--zookeeper** *{zk_host}:{port}*\ **/kafka** **--reassignment-json-file** *Path of the JSON file compiled in :ref:`8 <mrs_01_24534__li1230081019282>`* **--execute**

   If message "Successfully started reassignment of partitions" is displayed, the execution is successful.

.. |image1| image:: /_static/images/en-us_image_0000001583468825.png
