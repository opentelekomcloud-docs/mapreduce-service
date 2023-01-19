:original_name: mrs_01_24120.html

.. _mrs_01_24120:

Interconnecting FlinkServer with HBase
======================================

Scenario
--------

FlinkServer can be interconnected with HBase. The details are as follows:

-  It can be interconnected with dimension tables and sink tables.
-  When HBase and Flink are in the same cluster or clusters with mutual trust, FlinkServer can be interconnected with HBase.
-  If HBase and Flink are in different clusters without mutual trust, Flink in a normal cluster can be interconnected with HBase in a normal cluster.

Prerequisites
-------------

-  The HDFS, Yarn, Flink, and HBase services have been installed in a cluster.
-  The client that contains the HBase service has been installed, for example, in the **/opt/Bigdata/client** directory.

Procedure
---------

#. .. _mrs_01_24120__en-us_topic_0000001173471334_li197840151912:

   Log in to the node where the client is installed as the client installation user and copy all configuration files in the **/opt/Bigdata/client/HBase/hbase/conf/** directory of HBase to an empty directory of all nodes where FlinkServer is deployed, for example, **/tmp/client/HBase/hbase/conf/**.

   Change the owner of the configuration file directory and its upper-layer directory on the FlinkServer node to **omm**.

   **chown omm: /tmp/client/HBase/hbase/conf/ -R**

   .. note::

      -  FlinkServer nodes:

         Log in to Manager, choose **Cluster** > **Services** > **Flink** > **Instance**, and check the **Service IP Address** of FlinkServer.

      -  If the node where a FlinkServer instance is located is the node where the HBase client is installed, skip this step on this node.

#. Log in to Manager, choose **Cluster** > **Services** > **Flink** > **Configurations** > **All Configurations**, search for the **HBASE_CONF_DIR** parameter, and enter the FlinkServer directory (for example, **/tmp/client/HBase/hbase/conf/**) to which the HBase configuration files are copied in :ref:`1 <mrs_01_24120__en-us_topic_0000001173471334_li197840151912>` in **Value**.

   .. note::

      If the node where a FlinkServer instance is located is the node where the HBase client is installed, enter the **/opt/Bigdata/client/HBase/hbase/conf/** directory of HBase in **Value** of the **HBASE_CONF_DIR** parameter.

#. After the parameters are configured, click **Save**. After confirming the modification, click **OK**.

#. Click **Instance**, select all FlinkServer instances, choose **More** > **Restart Instance**, enter the password, and click **OK** to restart the instances.

#. Log in to Manager and choose **Cluster** > **Services** > **Flink**. In the **Basic Information** area, click the link on the right of **Flink WebUI** to access the Flink web UI.

#. Create a Flink SQL job and set Task Type to Stream job. For details, see :ref:`Creating a Job <mrs_01_24024__en-us_topic_0000001173470782_section1746418521537>`. On the job development page, configure the job parameters as follows and start the job.

   Select **Enable CheckPoint** in **Running Parameter** and set **Time Interval (ms)** to **60000**.

   The following example shows how to create a Flink SQL job:

   .. code-block::

      CREATE TABLE ksource1 (
      user_id STRING,
      item_id STRING,
      proctime as PROCTIME()
      ) WITH (
      'connector' = 'kafka',
      'topic' = 'ksource1',
      'properties.group.id' = 'group1',
      'properties.bootstrap.servers' = 'IP address of the Kafka broker instance 1:Kafka port number,IP address of the Kafka broker instance 2:Kafka port number',
      'format' = 'json',
      'properties.sasl.kerberos.service.name' = 'kafka'
      );

      CREATE TABLE hsink1 (
      rowkey STRING,
      f1 ROW < item_id STRING >,
      PRIMARY KEY (rowkey) NOT ENFORCED
      ) WITH (
      'connector' = 'hbase-2.2',
      'table-name' = 'dim_province',
      'zookeeper.quorum' = 'IP address of the ZooKeeper quorumpeer instance 1:ZooKeeper port number'IP address of the ZooKeeper quorumpeer instance 2:ZooKeeper port number'
      );

      INSERT INTO
      hsink1
      SELECT
      user_id as rowkey,
      ROW(item_id) as f1
      FROM
      ksource1;

   .. note::

      -  Kafka port number

         -  In security mode, the port number is the value of **sasl.port** (**21007** by default).

         -  In non-security mode, the port is the value of **port** (**9092** by default). If the port number is set to **9092**, set **allow.everyone.if.no.acl.found** to **true**. The procedure is as follows:

            Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Kafka**. On the displayed page, click **Configurations** and then **All Configurations**, search for **allow.everyone.if.no.acl.found**, set its value to **true**, and click **Save**.

      -  IP address of the ZooKeeper quorumpeer instance

         To obtain IP addresses of all ZooKeeper quorumpeer instances, log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Instance** and view the IP addresses of all the hosts where the quorumpeer instances locate.

      -  Port number of the ZooKeeper client

         Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the displayed page, click **Configurations** and check the value of **clientPort**. The default value is **24002**.

#. On the job management page, check whether the job status is **Running**.

#. Execute the following script to write data to Kafka. For details, see :ref:`Managing Messages in Kafka Topics <mrs_01_0379>`.

   **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates:Kafka port number* **--topic** **Topic name**

   For example, if the topic name is **ksource1**, the script is **sh kafka-console-producer.sh --broker-list** *IP address of the node where the Kafka instance locates*:*Kafka port number* **--topic ksource1**.

   Enter the message content.

   .. code-block::

      {"user_id": "3","item_id":"333333"},
      {"user_id": "4","item_id":"44444444"}

   Press **Enter** to send the message.

#. Log in to the HBase client and view the table data. For details, see :ref:`Using an HBase Client <mrs_01_24041>`.

   **hbase shel**

   **scan 'dim_province'**

Submitting a Job Using the Application
--------------------------------------

-  If the Flink run mode is used, you are advised to use the **export HBASE_CONF_DIR=** *HBase configuration directory*, for example, **export HBASE_CONF_DIR=/opt/hbaseconf**.
-  If the Flink run-application mode is used, you can use either of the following methods to submit jobs:

   -  (Recommended) Add the following configurations to a table creation statement.

      +---------------------------------------------------------+------------------------------------------------------------------+
      | Parameter                                               | Description                                                      |
      +=========================================================+==================================================================+
      | 'properties.hbase.rpc.protection' = 'authentication'    | This parameter must be consistent with that on the HBase server. |
      +---------------------------------------------------------+------------------------------------------------------------------+
      | 'properties.hbase.security.authorization' = 'true'      | Authentication is enabled.                                       |
      +---------------------------------------------------------+------------------------------------------------------------------+
      | 'properties.hbase.security.authentication' = 'kerberos' | Kerberos authentication is enabled.                              |
      +---------------------------------------------------------+------------------------------------------------------------------+

      Example:

      .. code-block::

         CREATE TABLE hsink1 (
              rowkey STRING,
              f1 ROW < q1 STRING >,
              PRIMARY KEY (rowkey) NOT ENFORCED
             ) WITH (
               'connector' = 'hbase-2.2',
               'table-name' = 'cc',
               'zookeeper.quorum' = 'x.x.x.x:24002',
               'properties.hbase.rpc.protection' = 'authentication',
               'properties.zookeeper.znode.parent' = '/hbase',
               'properties.hbase.security.authorization' = 'true',
               'properties.hbase.security.authentication' = 'kerberos'
            );

   -  Add the HBase configuration to YarnShip.

      Example: Dyarn.ship-files=/opt/hbaseconf
