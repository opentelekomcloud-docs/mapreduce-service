:original_name: mrs_01_24377.html

.. _mrs_01_24377:

Synchronizing Kafka Data to ClickHouse
======================================

This section describes how to create a Kafka table to automatically synchronize Kafka data to the ClickHouse cluster.

Prerequisites
-------------

-  You have created a Kafka cluster. The Kafka client has been installed.
-  You have created a ClickHouse cluster and installed the ClickHouse client. The ClickHouse and Kafka clusters are in the same VPC and can communicate with each other.

Constraints
-----------

Currently, ClickHouse cannot interconnect with Kafka clusters with security mode enabled.

.. _mrs_01_24377__section10908164973416:

Syntax of the Kafka Table
-------------------------

-  **Syntax**

   .. code-block::

      CREATE TABLE [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster]
      (
          name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1],
          name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2],
          ...
      ) ENGINE = Kafka()
      SETTINGS
          kafka_broker_list = 'host1:port1,host2:port2',
          kafka_topic_list = 'topic1,topic2,...',
          kafka_group_name = 'group_name',
          kafka_format = 'data_format';
          [kafka_row_delimiter = 'delimiter_symbol',]
          [kafka_schema = '',]
          [kafka_num_consumers = N]

-  **Parameter description**

   .. table:: **Table 1** Kafka table parameters

      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Mandatory             | Description                                                                                                                                                                                                                                                                               |
      +=======================+=======================+===========================================================================================================================================================================================================================================================================================+
      | kafka_broker_list     | Yes                   | A list of Kafka broker instances, separated by comma (,). For example, *IP address 1 of the Kafka broker instance*:**9092**,\ *IP address 2 of the Kafka broker instance*:**9092**,\ *IP address 3 of the Kafka broker instance*:**9092**.                                                |
      |                       |                       |                                                                                                                                                                                                                                                                                           |
      |                       |                       | .. note::                                                                                                                                                                                                                                                                                 |
      |                       |                       |                                                                                                                                                                                                                                                                                           |
      |                       |                       |    If the Kerberos authentication is enabled, parameter **allow.everyone.if.no.acl.found** must be set to **true** if port **21005** is used. Otherwise, an error will be reported.                                                                                                       |
      |                       |                       |                                                                                                                                                                                                                                                                                           |
      |                       |                       | To obtain the IP address of the Kafka broker instance, perform the following steps:                                                                                                                                                                                                       |
      |                       |                       |                                                                                                                                                                                                                                                                                           |
      |                       |                       | Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka**. Click **Instances** to query the IP addresses of the Kafka instances.                                                                                                  |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_topic_list      | Yes                   | A list of Kafka topics.                                                                                                                                                                                                                                                                   |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_group_name      | Yes                   | A group of Kafka consumers, which can be customized.                                                                                                                                                                                                                                      |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_format          | Yes                   | Kafka message format, for example, JSONEachRow, CSV, and XML.                                                                                                                                                                                                                             |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_row_delimiter   | No                    | Delimiter character, which ends a message.                                                                                                                                                                                                                                                |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_schema          | No                    | Parameter that must be used if the format requires a schema definition.                                                                                                                                                                                                                   |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka_num_consumers   | No                    | Number of consumers in per table. The default value is **1**. If the throughput of a consumer is insufficient, more consumers are required. The total number of consumers cannot exceed the number of partitions in a topic because only one consumer can be allocated to each partition. |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

How to Synchronize Kafka Data to ClickHouse
-------------------------------------------

#. .. _mrs_01_24377__li58847364569:

   Switch to the Kafka client installation directory. For details, see :ref:`Using the Kafka Client <mrs_01_1767>`.

   a. Log in to the node where the Kafka client is installed as the Kafka client installation user.

   b. Run the following command to go to the client installation directory:

      **cd /opt/client**

   c. Run the following command to configure environment variables:

      **source bigdata_env**

   d. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *Component service user*

#. .. _mrs_01_24377__li133267241488:

   Run the following command to create a Kafka topic. For details, see :ref:`Managing Kafka Topics <mrs_01_0376>`.

   **kafka-topics.sh --topic** *kafkacktest2* **--create --zookeeper** *IP address of the Zookeeper role instance:Port used by ZooKeeper to listen to client*\ **/kafka --partitions** *2* **--replication-factor** *1*

   .. note::

      -  **--topic** is the name of the topic to be created, for example, **kafkacktest2**.

      -  **--zookeeper** is the IP address of the node where the ZooKeeper role instances are located, which can be the IP address of any of the three role instances. You can obtain the IP address of the node by performing the following steps:

         Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**. View the IP addresses of the ZooKeeper role instances.

      -  **--partitions** and **--replication-factor** are the topic partitions and topic backup replicas, respectively. The number of the two parameters cannot exceed the number of Kafka role instances.

      -  To obtain the *Port used by ZooKeeper to listen to client*, log in to FusionInsight Manager, click **Cluster**, choose **Services** > **ZooKeeper**, and view the value of **clientPort** on the **Configuration** tab page. The default value is **24002**.

#. .. _mrs_01_24377__li64680261586:

   Log in to the ClickHouse client by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>`.

   a. Run the following command to go to the client installation directory:

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The user must have the permission to create ClickHouse tables. Therefore, you need to bind the corresponding role to the user. For details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *Component service user*

      Example: **kinit clickhouseuser**

   d. Run the following command to connect to the ClickHouse instance node to which data is to be imported:

      **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *Login username* **--password** **--port** *ClickHouse port number* **--database** *Database name* **--multiline**

      *Enter the user password.*

#. Create a Kafka table in ClickHouse by referring to :ref:`Syntax of the Kafka Table <mrs_01_24377__section10908164973416>`. For example, the following table creation statement is used to create a Kafka table whose name is **kafka_src_tbl3**, topic name is **kafkacktest2**, and message format is **JSONEachRow** in the default database.

   .. code-block::

      create table kafka_src_tbl3 on cluster default_cluster
      (id UInt32, age UInt32, msg String)
      ENGINE=Kafka()
      SETTINGS
       kafka_broker_list='IP address 1 of the Kafka broker instance:9092,IP address 2 of the Kafka broker instance:9092,IP address 3 of the Kafka broker instance:9092',
       kafka_topic_list='kafkacktest2',
       kafka_group_name='cg12',
       kafka_format='JSONEachRow';

#. Create a ClickHouse replicated table, for example, the ReplicatedMergeTree table named **kafka_dest_tbl3**.

   .. code-block::

      create table kafka_dest_tbl3 on cluster default_cluster
      ( id UInt32, age UInt32, msg String )
      engine = ReplicatedMergeTree('/clickhouse/tables/{shard}/default/kafka_dest_tbl3', '{replica}')
      partition by age
      order by id;

#. Create a materialized view, which converts data in Kafka in the background and saves the data to the created ClickHouse table.

   .. code-block::

      create materialized view consumer3 on cluster default_cluster to kafka_dest_tbl3 as select * from kafka_src_tbl3;

#. Perform :ref:`1 <mrs_01_24377__li58847364569>` again to go to the Kafka client installation directory.

#. Run the following command to send a message to the topic created in :ref:`2 <mrs_01_24377__li133267241488>`:

   **kafka-console-producer.sh --broker-list** *IP address 1 of the kafka broker instance*\ **:9092,**\ *IP address 2 of the kafka broker instance*\ **:9092,**\ *IP address 3 of the kafka broker instance*\ **:9092** **--topic** *kafkacktest2*

   .. code-block::

      >{"id":31, "age":30, "msg":"31 years old"}
      >{"id":32, "age":30, "msg":"31 years old"}
      >{"id":33, "age":30, "msg":"31 years old"}
      >{"id":35, "age":30, "msg":"31 years old"}

#. Use the ClickHouse client to log in to the ClickHouse instance node in :ref:`3 <mrs_01_24377__li64680261586>` and query the ClickHouse table data, for example, to query the replicated table **kafka_dest_tbl3**. It shows that the data in the Kafka message has been synchronized to this table.

   .. code-block::

      select * from kafka_dest_tbl3;

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001532676350.png
