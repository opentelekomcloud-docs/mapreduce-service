:original_name: mrs_01_24180.html

.. _mrs_01_24180:

Interconnecting FlinkServer with Hudi
=====================================

Scenario
--------

This section describes how to interconnect FlinkServer with Hudi through Flink SQL jobs.

Prerequisites
-------------

-  The HDFS, Yarn, Flink, and Hudi services have been installed in a cluster.
-  The client that contains the Hudi service has been installed, for example, in the **/opt/Bigdata/client** directory.
-  Flink 1.12.2 or later and Hudi 0.9.0 or later are required.
-  You have created a user with **FlinkServer Admin Privilege**, for example, **flink_admin**, to access the Flink web UI. For details, see :ref:`Authentication Based on Users and Roles <mrs_01_24049>`.

Flink Support for Read and Write Operations on Hudi Tables
----------------------------------------------------------

:ref:`Table 1 <mrs_01_24180__en-us_topic_0000001219149723_table1766417313461>` lists the read and write operations supported by Flink on Hudi COW and MOR tables.

.. _mrs_01_24180__en-us_topic_0000001219149723_table1766417313461:

.. table:: **Table 1** Flink support for read and write operations on Hudi tables

   ============ ========= =========
   Flink SQL    COW table MOR table
   ============ ========= =========
   Batch write  Supported Supported
   Batch read   Supported Supported
   Stream write Supported Supported
   Stream read  Supported Supported
   ============ ========= =========

.. note::

   Currently, Flink SQL allows you to read data from Hudi tables only in snapshot mode and read optimized mode.

Procedure
---------

#. Log in to Manager as user **flink_admin** and choose **Cluster** > **Services** > **Flink**. In the **Basic Information** area, click the link on the right of **Flink WebUI** to access the Flink web UI.

#. Create a Flink SQL job by referring to :ref:`Creating a Job <mrs_01_24024__en-us_topic_0000001173470782_section1746418521537>`. On the job development page, configure the job parameters as follows and start the job.

   Select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

   .. note::

      -  CheckPoint should be enabled on the Flink web UI because data is written to a Hudi table only when a Flink SQL job triggers CheckPoint. Adjust the CheckPoint interval based on service requirements. You are advised to set the interval to a large number.
      -  If the CheckPoint interval is too short, job exceptions may occur due to untimely data updates. It is recommended that the CheckPoint interval be configured at the minute level.
      -  Asynchronous compaction is required when a Flink SQL job writes an MOR table. For details about the parameter for controlling the compaction interval, visit Hudi official website https://hudi.apache.org/docs/configurations.html.

   -  The following shows a Flink SQL job writing data to an MOR table in stream mode. Only the Kafka JSON format is supported.

      .. code-block::

         CREATE TABLE stream_mor(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts INT,
         `p` VARCHAR(20)
         ) PARTITIONED BY (`p`) WITH (
         'connector' = 'hudi',
         'path' = 'hdfs://hacluster/tmp/hudi/stream_mor',
         'table.type' = 'MERGE_ON_READ'
         );

         CREATE TABLE kafka(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts INT,
         `p` VARCHAR(20)
         ) WITH (
         'connector' = 'kafka',
         'topic' = 'writehudi',
         'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
         'properties.group.id' = 'testGroup1',
         'scan.startup.mode' = 'latest-offset',
         'format' = 'json'
         );

         insert into
         stream_mor
         select
         *
         from
         kafka;

   -  The following shows a Flink SQL job writing data to a COW table in stream mode:

      .. code-block::

         CREATE TABLE stream_write_cow(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts INT,
         `p` VARCHAR(20)
         ) PARTITIONED BY (`p`) WITH (
         'connector' = 'hudi',
         'path' = 'hdfs://hacluster/tmp/hudi/stream_cow'
         );

         CREATE TABLE kafka(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts INT,
         `p` VARCHAR(20)
         ) WITH (
         'connector' = 'kafka',
         'topic' = 'writehudi',
         'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
         'properties.group.id' = 'testGroup1',
         'scan.startup.mode' = 'latest-offset',
         'format' = 'json'
         );

         insert into
         stream_write_cow
         select
         *
         from
         kafka;

   -  The following shows a Flink SQL job reading an MOR table.

      .. code-block::

         CREATE TABLE hudi_read_spark_mor(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts INT,
         `p` VARCHAR(20)
         ) PARTITIONED BY (`p`) WITH (
         'connector' = 'hudi',
         'path' = 'hdfs://hacluster/tmp/default/tb_hudimor',
         'table.type' = 'MERGE_ON_READ'
         );

         CREATE TABLE kafka(
         uuid VARCHAR(20),
         name VARCHAR(10),
         age INT,
         ts timestamp(6)INT,
         `p` VARCHAR(20)
         ) WITH (
         'connector' = 'kafka',
         'topic' = 'writehudi',
         'properties.bootstrap.servers' = 'IP address of the Kafka broker instance:Kafka port number',
         'properties.group.id' = 'testGroup1',
         'scan.startup.mode' = 'latest-offset',
         'format' = 'json'
         );

         insert into
         hudi_read_spark_mor
         select
         *
         from
         kafka;

   .. note::

      Kafka port number

      -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

      -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

         Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

#. After data is written to the Hudi table by a Flink SQL job and is read by Spark and Hive, use **run_hive_sync_tool.sh** to synchronize the data in the Hudi table to Hive. For details about the synchronization method, see :ref:`Synchronizing Hudi Table Data to Hive <mrs_01_24064>`.

   .. important::

      Ensure that no partition is added before the synchronization. After the synchronization, new partitions cannot be read.
