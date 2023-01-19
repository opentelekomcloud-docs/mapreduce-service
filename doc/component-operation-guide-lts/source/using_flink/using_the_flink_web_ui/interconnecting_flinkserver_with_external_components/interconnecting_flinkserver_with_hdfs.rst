:original_name: mrs_01_24247.html

.. _mrs_01_24247:

Interconnecting FlinkServer with HDFS
=====================================

Scenario
--------

This section describes the data definition language (DDL) of HDFS as a sink table, as well as the WITH parameters and example code for creating a sink table, and provides guidance on how to perform operations on the FlinkServer job management page.

If your Kafka cluster is in security mode, the following example SQL statements can be used.

Prerequisites
-------------

-  The HDFS, Yarn, and Flink services have been installed in a cluster.
-  The client that contains the HDFS service has been installed, for example, in the **/opt/Bigdata/client** directory.
-  You have created a user with **FlinkServer Admin Privilege**, for example, **flink_admin**, to access the Flink web UI. For details, see :ref:`Authentication Based on Users and Roles <mrs_01_24049>`.

Procedure
---------

#. Log in to Manager as user **flink_admin** and choose **Cluster** > **Services** > **Flink**. In the **Basic Information** area, click the link on the right of **Flink WebUI** to access the Flink web UI.

#. Create a Flink SQL job by referring to :ref:`Creating a Job <mrs_01_24024__en-us_topic_0000001173470782_section1746418521537>`. On the job development page, configure the job parameters as follows and start the job.

   Select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

   .. code-block::

      CREATE TABLE kafka_table (
        user_id STRING,
        order_amount DOUBLE,
        log_ts TIMESTAMP(3),
        WATERMARK FOR log_ts AS log_ts - INTERVAL '5' SECOND
      ) WITH (
        'connector' = 'kafka',
        'topic' = 'user_source',
        'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
        'properties.group.id' = 'testGroup',
        'scan.startup.mode' = 'latest-offset',
        'format' = 'csv',
         --Ignore the CSV data that fails to be parsed.
        'csv.ignore-parse-errors' = 'true' ,--If the data is in JSON format, set 'json.ignore-parse-errors' to true.
        'properties.sasl.kerberos.service.name' = 'kafka',
        'properties.security.protocol' = 'SASL_PLAINTEXT',
        'properties.kerberos.domain.name' = 'hadoop.System domain name'

      );

      CREATE TABLE fs_table (
        user_id STRING,
        order_amount DOUBLE,
        dt STRING,
        `hour` STRING
      ) PARTITIONED BY (dt, `hour`) WITH ( --Date-specific file partitioning
        'connector'='filesystem',
        'path'='hdfs:///sql/parquet',
        'format'='parquet',
        'sink.partition-commit.delay'='1 h',
        'sink.partition-commit.policy.kind'='success-file'
      );
      -- streaming sql, insert into file system table
      INSERT INTO fs_table SELECT user_id, order_amount, DATE_FORMAT(log_ts, 'yyyy-MM-dd'), DATE_FORMAT(log_ts, 'HH') FROM kafka_table;

   .. note::

      Kafka port number

      -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

      -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

         Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

#. On the job management page, check whether the job status is **Running**.

#. Execute the following commands to view the topic and write data to Kafka. For details, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

   **./kafka-topics.sh --list --zookeeper** *IP address of the ZooKeeper quorumpeer instance*:*ZooKeeper port number*\ **/kafka**

   **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic** *Topic name* --**producer.config** *Client directory*/**Kafka/kafka/config/producer.properties**

   For example, if the topic name is **user_source**, the script is **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic user_source** --**producer.config** **/opt/Bigdata/client/Kafka/kafka/config/producer.properties**.

   Enter the message content.

   .. code-block::

      3,3333,"2021-09-10 14:00"
      4,4444,"2021-09-10 14:01"

   Press **Enter** to send the message.

   .. note::

      -  IP address of the ZooKeeper quorumpeer instance

         To obtain IP addresses of all ZooKeeper quorumpeer instances, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Instance** and view the IP addresses of all the hosts where the quorumpeer instances locate.

      -  Port number of the ZooKeeper client

         Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the displayed page, click **Configurations** and check the value of **clientPort**. The default value is **24002**.

#. Run the following command to check whether data is written from the HDFS directory to the sink table:

   **hdfs dfs -ls -R /sql/parquet**

Interconnecting Flink with HDFS Partitions
------------------------------------------

-  Customized partitioning

   Flink's file system supports partitions in the standard Hive format. You do not need to register partitions with a table catalog. Partitions are inferred based on the directory structure.

   For example, a table that is partitioned based on the following directory is inferred to contain datetime and hour partitions.

   .. code-block::

      path
      └── datetime=2021-09-03
          └── hour=11
              ├── part-0.parquet
              ├── part-1.parquet
          └── hour=12
              ├── part-0.parquet
      └── datetime=2021-09-24
          └── hour=6
              ├── part-0.parquet

-  Rolling policy of partition files

   Data in the partition directories is split into part files. Each partition contains at least one part file, which is used to receive the data written by the subtask of the sink.

   The following parameters describe the rolling policies of partition files.

   +---------------------------------------+---------------+------------+---------------------------------------------------------------------------+
   | Parameter                             | Default Value | Type       | Description                                                               |
   +=======================================+===============+============+===========================================================================+
   | sink.rolling-policy.file-size         | 128 MB        | MemorySize | Maximum size of a partition file before it is rolled.                     |
   +---------------------------------------+---------------+------------+---------------------------------------------------------------------------+
   | sink.rolling-policy.rollover-interval | 30 minutes    | Duration   | Maximum duration that a partition file can stay open before it is rolled. |
   +---------------------------------------+---------------+------------+---------------------------------------------------------------------------+
   | sink.rolling-policy.check-interval    | 1 minute      | Duration   | Interval for checking time-based rolling policies.                        |
   +---------------------------------------+---------------+------------+---------------------------------------------------------------------------+

-  File merging

   File compression is supported, allowing applications to have a shorter checkpoint interval without generating a large number of files.

   .. note::

      Only files in a single checkpoint are compressed. That is, the number of generated files is at least the same as the number of checkpoints. Files are invisible before merged. They are visible after both the checkpoint and compression are complete. If file compression takes too much time, the checkpoint will be prolonged.

   +----------------------+---------------+------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Default Value | Type       | Description                                                                                                                                                                                                                               |
   +======================+===============+============+===========================================================================================================================================================================================================================================+
   | auto-compaction      | false         | Boolean    | Whether to enable automatic compression. Data will be written to temporary files. After a checkpoint is complete, the temporary files generated by the checkpoint are compressed. These temporary files are invisible before compression. |
   +----------------------+---------------+------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | compaction.file-size | none          | MemorySize | Size of the target file to be compressed. The default value is the size of the file to be rolled.                                                                                                                                         |
   +----------------------+---------------+------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Partition commit

   After a file is written to a partition, for example, a partition is added to Hive metastore (HMS) or a **\_SUCCESS** file is written to a directory, the downstream application needs to be notified. Triggers and policies are used to commit partition files.

   -  Trigger parameters for committing partition files

      +-------------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                     | Default Value   | Type            | Description                                                                                                                                                                                                                                                               |
      +===============================+=================+=================+===========================================================================================================================================================================================================================================================================+
      | sink.partition-commit.trigger | process-time    | String          | -  process-time: System time of the compute node. It does not need to extract the partition time or generate watermarks. If the current system time exceeds the system time generated when a partition is created plus the delay time, the partition should be submitted. |
      |                               |                 |                 | -  partition-time: Time extracted from the partition. Watermarks are required. If the time for generating watermarks exceeds the time extracted from a partition plus the delay time, the partition should be submitted.                                                  |
      +-------------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | sink.partition-commit.delay   | 0 s             | Duration        | Partitions will not be committed before the delay time. If it is a daily partition, the value is **1 d**. If it is an hourly one, the value is **1 h**.                                                                                                                   |
      +-------------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  Policy parameters for committing partition files

      +-----------------------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                               | Default Value   | Type            | Description                                                                                                                                                                |
      +=========================================+=================+=================+============================================================================================================================================================================+
      | sink.partition-commit.policy.kind       | ``-``           | String          | Policy for committing partitions:                                                                                                                                          |
      |                                         |                 |                 |                                                                                                                                                                            |
      |                                         |                 |                 | -  **metastore**: used to add partitions to metastore. Only Hive tables support the metastore policy. The file system manages partitions based on the directory structure. |
      |                                         |                 |                 | -  **success-file**: used to add **success-file** files to a directory.                                                                                                    |
      |                                         |                 |                 | -  The two policies can be configured at the same time, that is, **'sink.partition-commit.policy.kind'='metastore,success-file'**.                                         |
      +-----------------------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | sink.partition-commit.policy.class      | ``-``           | String          | Class that implements partition commit policy interfaces.                                                                                                                  |
      |                                         |                 |                 |                                                                                                                                                                            |
      |                                         |                 |                 | This parameter takes effect only in the customized submission policies.                                                                                                    |
      +-----------------------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | sink.partition-commit.success-file.name | \_SUCCESS       | String          | File name of the success-file partition commit policy. The default value is **\_SUCCESS**.                                                                                 |
      +-----------------------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
