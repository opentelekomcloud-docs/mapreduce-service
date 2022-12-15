:original_name: mrs_01_1061.html

.. _mrs_01_1061:

Typical Scenario: Collecting Local Static Logs and Uploading Them to Kafka
==========================================================================

Scenario
--------

This section describes how to use the Flume client to collect static logs from a local host and save them to the topic list (test1) of Kafka.

This section applies to MRS 3.\ *x* or later clusters.

.. note::

   By default, the cluster network environment is secure and the SSL authentication is not enabled during the data transmission process. For details about how to use the encryption mode, see :ref:`Configuring the Encrypted Transmission <mrs_01_1069>`. The configuration applies to scenarios where only the Flume is configured, for example, Spooldir Source+Memory Channel+Kafka Sink.

Prerequisites
-------------

-  The cluster has been installed, including the Kafka and Flume services.
-  The Flume client has been installed. For details, see `Installing the Flume Client <https://docs.otc.t-systems.com/cmpntguide/mrs/mrs_01_0392.html>`__.
-  The network environment of the cluster is secure.
-  The system administrator has understood service requirements and prepared Kafka administrator **flume_kafka**.

Procedure
---------

#. Set Flume parameters.

   Use the Flume configuration tool on Manager to configure the Flume role client parameters and generate a configuration file.

   a. Log in to FusionInsight Manager. Choose **Cluster** > **Services** > **Flume** > **Configuration Tool**.

   b. Set **Agent Name** to **client**. Select and drag the source, channel, and sink to be used to the GUI on the right, and connect them.

      Use SpoolDir Source, Memory Channel, and Kafka Sink.

   c. Double-click the source, channel, and sink. Set corresponding configuration parameters by referring to :ref:`Table 1 <mrs_01_1061__table1162101394616>` based on the actual environment.

      .. note::

         -  If you want to continue using the **properties.propretites** file by modifying it, log in to FusionInsight Manager, choose **Cluster** > **Services**. On the page that is displayed, choose **Flume**. On the displayed page, click the **Configuration Tool** tab, click **Import**, import the file, and modify the configuration items related to non-encrypted transmission.
         -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.

      .. _mrs_01_1061__table1162101394616:

      .. table:: **Table 1** Parameters to be modified for the Flume role client

         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Parameter               | Description                                                                                                                                                                                                    | Example Value                     |
         +=========================+================================================================================================================================================================================================================+===================================+
         | Name                    | The value must be unique and cannot be left blank.                                                                                                                                                             | test                              |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | spoolDir                | Specifies the directory where the file to be collected resides. This parameter cannot be left blank. The directory needs to exist and have the write, read, and execute permissions on the flume running user. | /srv/BigData/hadoop/data1/zb      |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | trackerDir              | Specifies the path for storing the metadata of files collected by Flume.                                                                                                                                       | /srv/BigData/hadoop/data1/tracker |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | batchSize               | Specifies the number of events that Flume sends in a batch (number of data pieces). A larger value indicates higher performance and lower timeliness.                                                          | 61200                             |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | kafka.topics            | Specifies the list of subscribed Kafka topics, which are separated by commas (,). This parameter cannot be left blank.                                                                                         | test1                             |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | kafka.bootstrap.servers | Specifies the bootstrap IP address and port list of Kafka. The default value is all Kafkabrokers in the Kafka cluster.                                                                                         | 192.168.101.10:21007              |
         +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+

   d. .. _mrs_01_1061__l14d98e844ee849a99592f46d8be65b86:

      Click **Export** to save the **properties.properties** configuration file to the local server.

#. Upload the configuration file.

   Upload the file exported in :ref:`1.d <mrs_01_1061__l14d98e844ee849a99592f46d8be65b86>` to the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf** directory of the cluster.

3. Verify log transmission.

   a. Log in to the Kafka client.

      **cd** *Kafka client installation directory*\ **/Kafka/kafka**

      **kinit flume_kafka** (Enter the password.)

   b. Read data from a Kafka topic.

      **bin/kafka-console-consumer.sh --topic** *topic name* **--bootstrap-server** *Kafka service IP address of the node where the role instance is located*\ **: 21007 --consumer.config config/consumer.properties --from-beginning**

      The system displays the contents of the file to be collected.

      .. code-block:: console

         [root@host1 kafka]# bin/kafka-console-consumer.sh --topic test1 --bootstrap-server 192.168.101.10:21007 --consumer.config config/consumer.properties --from-beginning
         Welcome to flume
