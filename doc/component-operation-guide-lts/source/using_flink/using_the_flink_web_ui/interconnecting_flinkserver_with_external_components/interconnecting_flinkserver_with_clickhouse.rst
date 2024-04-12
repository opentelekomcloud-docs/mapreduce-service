:original_name: mrs_01_24148.html

.. _mrs_01_24148:

Interconnecting FlinkServer with ClickHouse
===========================================

Scenario
--------

Flink interconnects with the ClickHouseBalancer instance of ClickHouse to read and write data, preventing ClickHouse traffic distribution problems.

.. important::

   When "FlinkSQL" is displayed in the command output on the FlinkServer web UI in MRS 3.2.0 or later clusters, the **password** field in the SQL statement is left blank to meet security requirements. Before you submit a job, manually enter the password.

Prerequisites
-------------

-  Services such as ClickHouse, HDFS, Yarn, Flink, and HBase have been installed in the cluster.
-  The client has been installed, for example, in **/opt/Bigdata/client**.

Mapping Between Flink SQL and ClickHouse Data Types
---------------------------------------------------

=================== ====================
Flink SQL Data Type ClickHouse Data Type
=================== ====================
BOOLEAN             UInt8
TINYINT             Int8
SMALLINT            Int16
INTEGER             Int32
BIGINT              Int64
FLOAT               Float32
DOUBLE              Float64
CHAR                String
VARCHAR             String
VARBINARY           FixedString
DATE                Date
TIMESTAMP           DateTime
DECIMAL             Decimal
=================== ====================

Procedure
---------

#. Log in to the node where the client is installed as user **root**.

#. Run the following command to go to the client installation directory:

   **cd /opt/Bigdata/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create ClickHouse tables. If Kerberos authentication is disabled for the current cluster, skip this step:

   **kinit** *Component service user*

   Example: **kinit** **clickhouseuser**

#. Connect to the ClickHouse client. For details, see :ref:`Using ClickHouse from Scratch <mrs_01_2345>`.

   -  Normal mode:

      **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *Username* **--password '**\ *Password*\ **'** **--port** *ClickHouse port number*

   -  Security mode:

      **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *Username* **--password '**\ *Password*\ **'--port** *ClickHouse port number* **--secure** **--multiline**

#. Run the following statements to create a replication table and a distributed table.

   a. Create a replication table **default.test1**.

      .. code-block::

         CREATE TABLE default.test1 on cluster default_cluster
         (
         `pid` Int8,
         `uid` UInt8,
         `Int_16` Int16,
         `Int_32` Int32,
         `Int_64` Int64,
         `String_x` String,
         `String_y` String,
         `float_32` Float32,
         `float_64` Float64,
         `Decimal_x` Decimal32(2),
         `Date_x` Date,
         `DateTime_x` DateTime
         )
         ENGINE = ReplicatedReplacingMergeTree('/clickhouse/tables/{shard}/test1','{replica}')
         PARTITION BY pid
         ORDER BY (pid, DateTime_x);

   b. Create a distributed table **test1_all**.

      .. code-block::

         CREATE TABLE test1_all ON CLUSTER default_cluster
         (
         `pid` Int8,
         `uid` UInt8,
         `Int_16` Int16,
         `Int_32` Int32,
         `Int_64` Int64,
         `String_x` String,
         `String_y` String,
         `float_32` Float32,
         `float_64` Float64,
         `Decimal_x` Decimal32(2),
         `Date_x` Date,
         `DateTime_x` DateTime
         )
         ENGINE = Distributed(default_cluster, default, test1, rand());

#. Log in to Manager and choose **Cluster** > **Services** > **Flink**. In the **Basic Information** area, click the link on the right of **Flink WebUI** to access the Flink web UI.

#. Create a Flink SQL job and set **Task Type** to **Stream job**. For details, see :ref:`Creating a Job <mrs_01_24024__en-us_topic_0000001173470782_section1746418521537>`. On the job development page, configure the job parameters as follows and start the job. Select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

   -  If the current MRS cluster is in security mode, perform the following operations:

      .. code-block::

         create table kafkasource(
         `pid` TINYINT,
         `uid` BOOLEAN,
         `Int_16` SMALLINT,
         `Int_32` INTEGER,
         `Int_64` BIGINT,
         `String_x` CHAR,
         `String_y` VARCHAR(10),
         `float_32` FLOAT,
         `float_64` DOUBLE,
         `Decimal_x` DECIMAL(9,2),
         `Date_x` DATE,
         `DateTime_x` TIMESTAMP
         ) with(
           'connector' = 'kafka',
           'topic' = 'input',
           'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
           'properties.group.id' = 'group1',
           'scan.startup.mode' = 'earliest-offset',
           'format' = 'json',
           'properties.sasl.kerberos.service.name' = 'kafka',
           'properties.security.protocol' = 'SASL_PLAINTEXT',
           'properties.kerberos.domain.name' = 'hadoop.System domain name'
         );
         CREATE TABLE cksink (
         `pid` TINYINT,
         `uid` BOOLEAN,
         `Int_16` SMALLINT,
         `Int_32` INTEGER,
         `Int_64` BIGINT,
         `String_x` CHAR,
         `String_y` VARCHAR(10),
         `float_32` FLOAT,
         `float_64` DOUBLE,
         `Decimal_x` DECIMAL(9,2),
         `Date_x` DATE,
         `DateTime_x` TIMESTAMP
         ) WITH (
         'connector' = 'jdbc',
         'url' = 'jdbc:clickhouse://ClickHouseBalancer instance IP address:21422/default?ssl=true&sslmode=none',
         'username' = 'ClickHouse user. For details, see the note below.',
         'password' = 'ClickHouse user password. For details, see the note below.',
         'table-name' = 'test1_all',
         'driver' = 'ru.yandex.clickhouse.ClickHouseDriver',
         'sink.buffer-flush.max-rows' = '0',
         'sink.buffer-flush.interval' = '60s'
         );
         Insert into cksink
         select
         *
         from
         kafkasource;

   -  If the current MRS cluster is in normal mode, perform the following operations:

      .. code-block::

         create table kafkasource(
         `pid` TINYINT,
         `uid` BOOLEAN,
         `Int_16` SMALLINT,
         `Int_32` INTEGER,
         `Int_64` BIGINT,
         `String_x` CHAR,
         `String_y` VARCHAR(10),
         `float_32` FLOAT,
         `float_64` DOUBLE,
         `Decimal_x` DECIMAL(9,2),
         `Date_x` DATE,
         `DateTime_x` TIMESTAMP
         ) with(
           'connector' = 'kafka',
           'topic' = 'kinput',
           'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
           'properties.group.id' = 'kafka_test',
           'scan.startup.mode' = 'earliest-offset',
           'format' = 'json'
         );
         CREATE TABLE cksink (
         `pid` TINYINT,
         `uid` BOOLEAN,
         `Int_16` SMALLINT,
         `Int_32` INTEGER,
         `Int_64` BIGINT,
         `String_x` CHAR,
         `String_y` VARCHAR(10),
         `float_32` FLOAT,
         `float_64` DOUBLE,
         `Decimal_x` DECIMAL(9,2),
         `Date_x` DATE,
         `DateTime_x` TIMESTAMP
         ) WITH (
         'connector' = 'jdbc',
         'url' = 'jdbc:clickhouse://ClickHouseBalancer instance IP address:21425/default',
         'table-name' = 'test1_all',
         'driver' = 'ru.yandex.clickhouse.ClickHouseDriver',
         'sink.buffer-flush.max-rows' = '0',
         'sink.buffer-flush.interval' = '60s'
         );
         Insert into cksink
         select
         *
         from
         kafkasource;

   .. note::

      -  If an MRS cluster is in the security mode, the user in the **cksink** table must have related permissions on the ClickHouse tables. For details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`.

      -  Kafka port number

         -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

         -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

            Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

      -  **21422**: HTTPS port number of the ClickHouseBalancer instance IP address.

      -  **21425**: HTTP port number of the ClickHouseBalancer instance IP address.

      -  Parameters for batch write: Flink stores data in the memory and then flushes the data to the database table when the trigger condition is met. The configurations are as follows:

         **sink.buffer-flush.max-rows**: Number of rows written to ClickHouse. The default value is **100**.

         **sink.buffer-flush.interval**: Interval for batch write. The default value is **1s**.

         If either of the two conditions is met, a sink operation is triggered. That is, data will be flushed to the database table.

         -  Scenario 1: sink every 60s

            'sink.buffer-flush.max-rows' = '0',

            'sink.buffer-flush.interval' = '60s'

         -  Scenario 2: sink every 100 rows

            'sink.buffer-flush.max-rows' = '100',

            'sink.buffer-flush.interval' = '0s'

         -  Scenario 3: no sink

            'sink.buffer-flush.max-rows' = '0',

            'sink.buffer-flush.interval' = '0s'

#. On the job management page, check whether the job status is **Running**.

#. Execute the following script to write data to Kafka. For details, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

   **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--**\ **topic**\ *Topic name* **--producer.config ../config/producer.properties**

   For example, if the topic name is **kinput**, the script is **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic kinput** **--producer.config ../config/producer.properties**.

   Enter the message content.

   .. code-block::

      {"pid": "3","uid":false,"Int_16": "6533","Int_32": "429496294","Int_64": "1844674407370955614","String_x": "abc1","String_y": "abc1defghi","float_32": "0.1234","float_64": "95.1","Decimal_x": "0.451236414","Date_x": "2021-05-29","DateTime_x": "2021-05-21 10:05:10"},
      {"pid": "4","uid":false,"Int_16": "6533","Int_32": "429496294","Int_64": "1844674407370955614","String_x": "abc1","String_y": "abc1defghi","float_32": "0.1234","float_64": "95.1","Decimal_x": "0.4512314","Date_x": "2021-05-29","DateTime_x": "2021-05-21 10:05:10"}

   Press **Enter** to send the message.

#. Interconnect with ClickHouse to query the table data.

   **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *Username* **--password '**\ *Password*\ **'--port** *ClickHouse port number* **--secure** **--multiline**

   Run the following command to check whether data is written to a specified ClickHouse table, for example, **test1_all**.

   **select \* from test1_all;**
