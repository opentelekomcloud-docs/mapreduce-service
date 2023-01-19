:original_name: mrs_01_24179.html

.. _mrs_01_24179:

Interconnecting FlinkServer with Hive
=====================================

Scenario
--------

Currently, FlinkServer interconnects with Hive MetaStore. Therefore, the MetaStore function must be enabled for Hive. Hive can be used as source, sink, and dimension tables.

If your Kafka cluster is in security mode, the following example SQL statements can be used.

Prerequisites
-------------

-  Services such as HDFS, Yarn, Kafka, Flink, and Hive have been installed in the cluster.
-  The client that contains the Hive service has been installed, for example, in the **/opt/Bigdata/client** directory.
-  Flink 1.12.2 or later and Hive 3.1.0 or later are supported.
-  You have created a user with **FlinkServer Admin Privilege**, for example, **flink_admin**, to access the Flink web UI. For details, see :ref:`Authentication Based on Users and Roles <mrs_01_24049>`.
-  You have obtained the client configuration file and credential of the user for accessing the Flink web UI. For details, see "Note" in :ref:`Creating a Cluster Connection <mrs_01_24021__en-us_topic_0000001173789648_section878113401693>`.

Procedure
---------

The following uses the process of interconnecting a Kafka mapping table to Hive as an example.

#. Log in to the Flink web UI as user **flink_admin**. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. .. _mrs_01_24179__en-us_topic_0000001173470662_li159021532193916:

   Create a cluster connection, for example, **flink_hive**.

   a. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.

   b. Click **Create Cluster Connection**. On the displayed page, enter information by referring to :ref:`Table 1 <mrs_01_24179__en-us_topic_0000001173470662_table134890201518>` and click **Test**. After the test is successful, click **OK**.

      .. _mrs_01_24179__en-us_topic_0000001173470662_table134890201518:

      .. table:: **Table 1** Parameters for creating a cluster connection

         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Parameter               | Description                                                                                                                                                                                | Example Value                      |
         +=========================+============================================================================================================================================================================================+====================================+
         | Cluster Connection Name | Name of the cluster connection, which can contain a maximum of 100 characters. Only letters, digits, and underscores (_) are allowed.                                                      | flink_hive                         |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Description             | Description of the cluster connection name.                                                                                                                                                | ``-``                              |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Version                 | Select a cluster version.                                                                                                                                                                  | MRS 3                              |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Secure Version          | -  If the secure version is used, select **Yes** for a security cluster. Enter the username and upload the user credential.                                                                | Yes                                |
         |                         | -  If not, select **No**.                                                                                                                                                                  |                                    |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Username                | The user must have the minimum permissions for accessing services in the cluster. The name can contain a maximum of 100 characters. Only letters, digits, and underscores (_) are allowed. | flink_admin                        |
         |                         |                                                                                                                                                                                            |                                    |
         |                         | This parameter is available only when **Secure Version** is set to **Yes**.                                                                                                                |                                    |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | Client Profile          | Client profile of the cluster, in TAR format.                                                                                                                                              | ``-``                              |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
         | User Credential         | User authentication credential in FusionInsight Manager in TAR format.                                                                                                                     | User credential of **flink_admin** |
         |                         |                                                                                                                                                                                            |                                    |
         |                         | This parameter is available only when **Secure Version** is set to **Yes**.                                                                                                                |                                    |
         |                         |                                                                                                                                                                                            |                                    |
         |                         | Files can be uploaded only after the username is entered.                                                                                                                                  |                                    |
         +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------+

#. Create a Flink SQL job, for example, **flinktest1**.

   a. Click **Job Management**. The job management page is displayed.

   b. Click **Create Job**. On the displayed job creation page, set parameters by referring to :ref:`Table 2 <mrs_01_24179__en-us_topic_0000001173470662_table25451917135812>` and click **OK**. The job development page is displayed.

      .. _mrs_01_24179__en-us_topic_0000001173470662_table25451917135812:

      .. table:: **Table 2** Parameters for creating a job

         +-------------+----------------------------------------------------------------------------------------------------------------+---------------+
         | Parameter   | Description                                                                                                    | Example Value |
         +=============+================================================================================================================+===============+
         | Type        | Job type, which can be **Flink SQL** or **Flink Jar**.                                                         | Flink SQL     |
         +-------------+----------------------------------------------------------------------------------------------------------------+---------------+
         | Name        | Job name, which can contain a maximum of 64 characters. Only letters, digits, and underscores (_) are allowed. | flinktest1    |
         +-------------+----------------------------------------------------------------------------------------------------------------+---------------+
         | Task Type   | Type of the job data source, which can be a stream job or a batch job.                                         | Stream job    |
         +-------------+----------------------------------------------------------------------------------------------------------------+---------------+
         | Description | Job description, which can contain a maximum of 100 characters.                                                | ``-``         |
         +-------------+----------------------------------------------------------------------------------------------------------------+---------------+

#. On the job development page, enter the following statements and click **Check Semantic** to check the input content.

   .. code-block::

      CREATE TABLE test_kafka (
        user_id varchar,
        item_id varchar,
        cat_id varchar,
        zw_test timestamp
      ) WITH (
        'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
        'format' = 'json',
        'topic' = 'zw_tset_kafka',
        'connector' = 'kafka',
        'scan.startup.mode' = 'latest-offset',
        'properties.sasl.kerberos.service.name' = 'kafka',
        'properties.security.protocol' = 'SASL_PLAINTEXT',
        'properties.kerberos.domain.name' = 'hadoop.System domain name'

      );
      CREATE CATALOG myhive WITH (
        'type' = 'hive',
        'hive-version' = '3.1.0',
        'default-database' = 'default',
        'cluster.name' = 'flink_hive'
      );
      use catalog myhive;
      set table.sql-dialect = hive;create table user_behavior_hive_tbl_no_partition (
          user_id STRING,
          item_id STRING,
          cat_id STRING,
          ts timestamp
        ) PARTITIONED BY (dy STRING, ho STRING, mi STRING) stored as textfile TBLPROPERTIES (
          'partition.time-extractor.timestamp-pattern' = '$dy $ho:$mi:00',
          'sink.partition-commit.trigger' = 'process-time',
          'sink.partition-commit.delay' = '0S',
          'sink.partition-commit.policy.kind' = 'metastore,success-file'
        );
      INSERT into
        user_behavior_hive_tbl_no_partition
      SELECT
        user_id,
        item_id,
        cat_id,
        zw_test,
        DATE_FORMAT(zw_test, 'yyyy-MM-dd'),
        DATE_FORMAT(zw_test, 'HH'),
        DATE_FORMAT(zw_test, 'mm')
      FROM
        default_catalog.default_database.test_kafka;

   .. note::

      -  Kafka port number

         -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

         -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

            Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

      -  The value of **'cluster.name'** is the name of the cluster connection created in :ref:`2 <mrs_01_24179__en-us_topic_0000001173470662_li159021532193916>`.

#. After the job is developed, select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

#. Click **Submit** in the upper left corner to submit the job.

#. After the job is successfully executed, choose **More** > **Job Monitoring** to view the job running details.

#. Execute the following commands to view the topic and write data to Kafka. For details, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

   **./kafka-topics.sh --list --zookeeper** *IP address of the ZooKeeper quorumpeer instance*:*ZooKeeper port number*\ **/kafka**

   **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic** *Topic name* --**producer.config** *Client directory*/**Kafka/kafka/config/producer.properties**

   For example, if the topic name is **zw_tset_kafka**, the script is **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic zw_tset_kafka** --**producer.config** **/opt/Bigdata/client/Kafka/kafka/config/producer.properties**.

   Enter the message content.

   .. code-block::

      {"user_id": "3","item_id":"333333","cat_id":"cat333","zw_test":"2021-09-08 09:08:01"}
      {"user_id": "4","item_id":"444444","cat_id":"cat444","zw_test":"2021-09-08 09:08:01"}

   Press **Enter** to send the message.

   .. note::

      -  IP address of the ZooKeeper quorumpeer instance

         To obtain IP addresses of all ZooKeeper quorumpeer instances, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Instance** and view the IP addresses of all the hosts where the quorumpeer instances locate.

      -  Port number of the ZooKeeper client

         Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the displayed page, click **Configurations** and check the value of **clientPort**. The default value is **24002**.

#. Run the following command to check whether data is written from the Hive table to the sink table:

   **beeline**

   **select \* from user_behavior_hive_tbl_no_partition;**
