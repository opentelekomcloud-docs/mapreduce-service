:original_name: mrs_01_24248.html

.. _mrs_01_24248:

Interconnecting FlinkServer with Kafka
======================================

Scenario
--------

This section describes the data definition language (DDL) of Kafka as a source or sink table, as well as the WITH parameters and example code for creating a table, and provides guidance on how to perform operations on the FlinkServer job management page.

If your Kafka cluster is in security mode, the following example SQL statements can be used.

Prerequisites
-------------

-  The HDFS, Yarn, Kafka, and Flink services have been installed in a cluster.
-  The client that contains the Kafka service has been installed, for example, in the **/opt/Bigdata/client** directory.
-  You have created a user with **FlinkServer Admin Privilege**, for example, **flink_admin**, to access the Flink web UI. For details, see :ref:`Authentication Based on Users and Roles <mrs_01_24049>`.

Procedure
---------

#. Log in to Manager as user **flink_admin** and choose **Cluster** > **Services** > **Flink**. In the **Basic Information** area, click the link on the right of **Flink WebUI** to access the Flink web UI.

#. Create a Flink SQL job by referring to :ref:`Creating a Job <mrs_01_24024__en-us_topic_0000001173470782_section1746418521537>`. On the job development page, configure the job parameters as follows and start the job.

   Select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

   .. code-block::

      CREATE TABLE KafkaSource (
        `user_id` VARCHAR,
        `user_name` VARCHAR,
        `age` INT
      ) WITH (
        'connector' = 'kafka',
        'topic' = 'test_source',
        'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
        'properties.group.id' = 'testGroup',
        'scan.startup.mode' = 'latest-offset',
        'format' = 'csv',
        'properties.sasl.kerberos.service.name' = 'kafka',
        'properties.security.protocol' = 'SASL_PLAINTEXT',
        'properties.kerberos.domain.name' = 'hadoop.System domain name'
      );
      CREATE TABLE KafkaSink(
        `user_id` VARCHAR,
        `user_name` VARCHAR,
        `age` INT
      ) WITH (
        'connector' = 'kafka',
        'topic' = 'test_sink',
        'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
        'scan.startup.mode' = 'latest-offset',
        'value.format' = 'csv',
        'properties.sasl.kerberos.service.name' = 'kafka',
        'properties.security.protocol' = 'SASL_PLAINTEXT',
        'properties.kerberos.domain.name' = 'hadoop.System domain name'
      );
      Insert into
        KafkaSink
      select
        *
      from
        KafkaSource;

   .. note::

      Kafka port number

      -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

      -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

         Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

#. On the job management page, check whether the job status is **Running**.

#. Execute the following commands to view the topic and write data to Kafka. For details, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

   **./kafka-topics.sh --list --zookeeper** *IP address of the ZooKeeper quorumpeer instance*:*ZooKeeper port number*\ **/kafka**

   **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic** *Topic name* --**producer.config** *Client directory*/**Kafka/kafka/config/producer.properties**

   For example, if the topic name is **test_source**, the script is **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic test_source** --**producer.config** **/opt/Bigdata/client/Kafka/kafka/config/producer.properties**.

   Enter the message content.

   .. code-block::

      1,clw,33

   Press **Enter** to send the message.

   .. note::

      -  IP address of the ZooKeeper quorumpeer instance

         To obtain IP addresses of all ZooKeeper quorumpeer instances, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Instance** and view the IP addresses of all the hosts where the quorumpeer instances locate.

      -  Port number of the ZooKeeper client

         Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the displayed page, click **Configurations** and check the value of **clientPort**. The default value is **24002**.

#. Run the following commands to check whether data is written from the Kafka topic to the sink table:

   **sh kafka-console-consumer.sh --topic** *Topic name* **--bootstrap-server** *IP address of the Kafka broker instance*:**Kafka port number** --**consumer.config /opt/Bigdata/client/Kafka/kafka/config/consumer.properties**

WITH Parameters
---------------

+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter                    | Mandatory                                  | Type            | Description                                                                                                                                                                                                              |
+==============================+============================================+=================+==========================================================================================================================================================================================================================+
| connector                    | Yes                                        | String          | Connector to be used. **kafka** is used for Kafka.                                                                                                                                                                       |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| topic                        | -  Yes (Kafka functions as a sink table.)  | String          | Topic name.                                                                                                                                                                                                              |
|                              | -  No (Kafka functions as a source table.) |                 |                                                                                                                                                                                                                          |
|                              |                                            |                 | -  When the Kafka is used as a source table, this parameter indicates the name of the topic from which data is read. Topic list is supported. Topics are separated by semicolons (;), for example, **Topic-1; Topic-2**. |
|                              |                                            |                 | -  When Kafka is used as a sink table, this parameter indicates the name of the topic to which data is written. Topic list is not supported for sinks.                                                                   |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| topic-pattern                | No (Kafka functions as a source table.)    | String          | Topic pattern.                                                                                                                                                                                                           |
|                              |                                            |                 |                                                                                                                                                                                                                          |
|                              |                                            |                 | This parameter is available when Kafka is used as a source table. The topic name must be a regular expression.                                                                                                           |
|                              |                                            |                 |                                                                                                                                                                                                                          |
|                              |                                            |                 | .. note::                                                                                                                                                                                                                |
|                              |                                            |                 |                                                                                                                                                                                                                          |
|                              |                                            |                 |    **topic-pattern** and **topic** cannot be set at the same time.                                                                                                                                                       |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| properties.bootstrap.servers | Yes                                        | String          | List of Kafka brokers, which are separated by commas (,).                                                                                                                                                                |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| properties.group.id          | Yes (Kafka functions as a source table.)   | String          | Kafka user group ID.                                                                                                                                                                                                     |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| format                       | Yes                                        | String          | Format of the value used for deserializing and serializing Kafka messages.                                                                                                                                               |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| properties.\*                | No                                         | String          | Authentication-related parameters that need to be added in security mode.                                                                                                                                                |
+------------------------------+--------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
