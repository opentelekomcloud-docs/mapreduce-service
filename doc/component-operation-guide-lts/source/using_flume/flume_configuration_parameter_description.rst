:original_name: mrs_01_0396.html

.. _mrs_01_0396:

Flume Configuration Parameter Description
=========================================

Some parameters can be configured on Manager.

Overview
--------

This section describes how to configure the sources, channels, and sinks of Flume, and modify the configuration items of each module.

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Flume**. On the displayed page, click the **Configuration Tool** tab to configure the **source**, **channel**, and **sink** parameters. Parameters such as **channels** and **type** are configured only in the client configuration file **properties.properties**, the path of which is *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume version*\ **/conf/properties.properties**.

.. note::

   You must input encrypted information for some configurations. For details on how to encrypt information, see :ref:`Using the Encryption Tool of the Flume Client <mrs_01_0395>`.

Common Source Configurations
----------------------------

-  **Avro Source**

   An Avro source listens to the Avro port, receives data from the external Avro client, and places data into configured channels. :ref:`Table 1 <mrs_01_0396__en-us_topic_0000001173949378_tb4f2cc56cf3945f7bba26f90f1afaa79>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_tb4f2cc56cf3945f7bba26f90f1afaa79:

   .. table:: **Table 1** Common configurations of an Avro source

      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Default Value         | Description                                                                                                                                                                           |
      +=======================+=======================+=======================================================================================================================================================================================+
      | channels              | **-**                 | Specifies the channel connected to the source. Multiple channels can be configured. Use spaces to separate them.                                                                      |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | In a single proxy process, sources and sinks are connected through channels. A source instance corresponds to multiple channels, but a sink instance corresponds only to one channel. |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | The format is as follows:                                                                                                                                                             |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | **<Agent >.sources.<Source>.channels = <channel1> <channel2> <channel3>...**                                                                                                          |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | **<Agent >.sinks.<Sink>.channels = <channel1>**                                                                                                                                       |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | This parameter can be configured only in the **properties.properties** file.                                                                                                          |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                  | avro                  | Specifies the type, which is set to **avro**. The type of each source is a fixed value.                                                                                               |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | This parameter can be configured only in the **properties.properties** file.                                                                                                          |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | bind                  | ``-``                 | Specifies the host name or IP address associated with the source.                                                                                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | port                  | ``-``                 | Specifies the bound port number.                                                                                                                                                      |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ssl                   | false                 | Specifies whether to use SSL encryption.                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                       |
      |                       |                       | -  true                                                                                                                                                                               |
      |                       |                       | -  false                                                                                                                                                                              |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | truststore-type       | JKS                   | Specifies the Java trust store type. Set this parameter to **JKS** or other truststore types supported by Java.                                                                       |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | truststore            | ``-``                 | Specifies the Java trust store file.                                                                                                                                                  |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | truststore-password   | ``-``                 | Specifies the Java trust store password.                                                                                                                                              |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keystore-type         | JKS                   | Specifies the key storage type. Set this parameter to **JKS** or other truststore types supported by Java.                                                                            |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keystore              | ``-``                 | Specifies the key storage file.                                                                                                                                                       |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keystore-password     | ``-``                 | Specifies the key storage password.                                                                                                                                                   |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **SpoolDir Source**

   A SpoolDir source monitors and transmits new files that have been added to directories in quasi-real-time mode. Common configurations are as follows:

   .. table:: **Table 2** Common configurations of a SpoolDir source

      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                  | Default Value         | Description                                                                                                                                                                                                                                              |
      +============================+=======================+==========================================================================================================================================================================================================================================================+
      | channels                   | ``-``                 | Specifies the channel connected to the source. Multiple channels can be configured.                                                                                                                                                                      |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | This parameter can be configured only in the **properties.properties** file.                                                                                                                                                                             |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                       | spooldir              | Type, which is set to **spooldir**.                                                                                                                                                                                                                      |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | This parameter can be configured only in the **properties.properties** file.                                                                                                                                                                             |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime                    | 0 (Disabled)          | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the source is restarted. Unit: second                                                                                                                             |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | spoolDir                   | ``-``                 | Specifies the monitoring directory.                                                                                                                                                                                                                      |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | fileSuffix                 | .COMPLETED            | Specifies the suffix added after file transmission is complete.                                                                                                                                                                                          |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | deletePolicy               | never                 | Specifies the source file deletion policy after file transmission is complete. The value can be either **never** or **immediate**.                                                                                                                       |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ignorePattern              | ^$                    | Specifies the regular expression of a file to be ignored.                                                                                                                                                                                                |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | trackerDir                 | .flumespool           | Specifies the metadata storage path during data transmission.                                                                                                                                                                                            |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | batchSize                  | 1000                  | Specifies the source transmission granularity.                                                                                                                                                                                                           |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | decodeErrorPolicy          | FAIL                  | Specifies the code error policy. This parameter can be configured only in the **properties.properties** file.                                                                                                                                            |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | The value can be **FAIL**, **REPLACE**, or **IGNORE**.                                                                                                                                                                                                   |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | **FAIL**: Generate an exception and fail the parsing.                                                                                                                                                                                                    |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | **REPLACE**: Replace the characters that cannot be identified with other characters, such as U+FFFD.                                                                                                                                                     |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | **IGNORE**: Discard character strings that cannot be parsed.                                                                                                                                                                                             |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | .. note::                                                                                                                                                                                                                                                |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       |    If a code error occurs in the file, set **decodeErrorPolicy** to **REPLACE** or **IGNORE**. Flume will skip the code error and continue to collect subsequent logs.                                                                                   |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | deserializer               | LINE                  | Specifies the file parser. The value can be either **LINE** or **BufferedLine**.                                                                                                                                                                         |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | -  When the value is set to **LINE**, characters read from the file are transcoded one by one.                                                                                                                                                           |
      |                            |                       | -  When the value is set to **BufferedLine**, one line or multiple lines of characters read from the file are transcoded in batches, which delivers better performance.                                                                                  |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | deserializer.maxLineLength | 2048                  | Specifies the maximum length for resolution by line, ranging from 0 to 2,147,483,647.                                                                                                                                                                    |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | deserializer.maxBatchLine  | 1                     | Specifies the maximum number of lines for resolution by line. If multiple lines are set, **maxLineLength** must be set to a corresponding multiplier. For example, if **maxBatchLine** is set to **2**, **maxLineLength** is set to **4096** (2048 x 2). |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | selector.type              | replicating           | Specifies the selector type. The value can be either **replicating** or **multiplexing**.                                                                                                                                                                |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | -  **replicating** indicates that the same content is sent to each channel.                                                                                                                                                                              |
      |                            |                       | -  **multiplexing** indicates that the content is sent only to certain channels according to the distribution rule.                                                                                                                                      |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | interceptors               | ``-``                 | Specifies the interceptor. For details, see the `Flume official document <https://flume.apache.org/FlumeUserGuide.html#flume-interceptors>`__.                                                                                                           |
      |                            |                       |                                                                                                                                                                                                                                                          |
      |                            |                       | This parameter can be configured only in the **properties.properties** file.                                                                                                                                                                             |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The Spooling source ignores the last line feed character of each event when data is read by line. Therefore, Flume does not calculate the data volume counters used by the last line feed character.

-  **Kafka Source**

   A Kafka source consumes data from Kafka topics. Multiple sources can consume data of the same topic, and the sources consume different partitions of the topic. Common configurations are as follows:

   .. table:: **Table 3** Common configurations of a Kafka source

      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                       | Default Value                             | Description                                                                                                                                                                        |
      +=================================+===========================================+====================================================================================================================================================================================+
      | channels                        | ``-``                                     | Specifies the channel connected to the source. Multiple channels can be configured.                                                                                                |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be configured only in the **properties.properties** file.                                                                                                       |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                            | org.apache.flume.source.kafka.KafkaSource | Specifies the type, which is set to **org.apache.flume.source.kafka.KafkaSource**.                                                                                                 |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be configured only in the **properties.properties** file.                                                                                                       |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime                         | 0 (Disabled)                              | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the source is restarted. Unit: second                                                       |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | nodatatime                      | 0 (Disabled)                              | Specifies the alarm threshold. An alarm is triggered when the duration that Kafka does not release data to subscribers exceeds the threshold. Unit: second                         |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | batchSize                       | 1000                                      | Specifies the number of events written into a channel at a time.                                                                                                                   |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | batchDurationMillis             | 1000                                      | Specifies the maximum duration of topic data consumption at a time, expressed in milliseconds.                                                                                     |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keepTopicInHeader               | false                                     | Specifies whether to save topics in the event header. If topics are saved, topics configured in Kafka sinks become invalid.                                                        |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | -  true                                                                                                                                                                            |
      |                                 |                                           | -  false                                                                                                                                                                           |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be configured only in the **properties.properties** file.                                                                                                       |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keepPartitionInHeader           | false                                     | Specifies whether to save partition IDs in the event header. If partition IDs are saved, Kafka sinks write data to the corresponding partitions.                                   |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | -  true                                                                                                                                                                            |
      |                                 |                                           | -  false                                                                                                                                                                           |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be set only in the properties.properties file.                                                                                                                  |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.bootstrap.servers         | ``-``                                     | Specifies the list of Broker addresses, which are separated by commas.                                                                                                             |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.consumer.group.id         | ``-``                                     | Specifies the Kafka consumer group ID.                                                                                                                                             |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.topics                    | ``-``                                     | Specifies the list of subscribed Kafka topics, which are separated by commas (,).                                                                                                  |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.topics.regex              | ``-``                                     | Specifies the subscribed topics that comply with regular expressions. **kafka.topics.regex** has a higher priority than **kafka.topics** and will overwrite **kafka.topics**.      |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.security.protocol         | SASL_PLAINTEXT                            | Specifies the security protocol of Kafka. The value must be set to **PLAINTEXT** for clusters in which Kerberos authentication is disabled.                                        |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.kerberos.domain.name      | ``-``                                     | Specifies the value of **default_realm** of Kerberos in the Kafka cluster, which should be configured only for security clusters.                                                  |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be set only in the properties.properties file.                                                                                                                  |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Other Kafka Consumer Properties | ``-``                                     | Specifies other Kafka configurations. This parameter can be set to any consumption configuration supported by Kafka, and the **.kafka** prefix must be added to the configuration. |
      |                                 |                                           |                                                                                                                                                                                    |
      |                                 |                                           | This parameter can be set only in the properties.properties file.                                                                                                                  |
      +---------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Taildir Source**

   A Taildir source monitors file changes in a directory and automatically reads the file content. In addition, it can transmit data in real time. :ref:`Table 4 <mrs_01_0396__en-us_topic_0000001173949378_t2c85090722c4451682fad2657a7bdc35>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_t2c85090722c4451682fad2657a7bdc35:

   .. table:: **Table 4** Common configurations of a Taildir source

      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                              | Default Value         | Description                                                                                                                                                                                                                                                  |
      +========================================+=======================+==============================================================================================================================================================================================================================================================+
      | channels                               | ``-``                 | Specifies the channel connected to the source. Multiple channels can be configured.                                                                                                                                                                          |
      |                                        |                       |                                                                                                                                                                                                                                                              |
      |                                        |                       | This parameter can be set only in the properties.properties file.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                                   | taildir               | Specifies the type, which is set to **taildir**.                                                                                                                                                                                                             |
      |                                        |                       |                                                                                                                                                                                                                                                              |
      |                                        |                       | This parameter can be set only in the properties.properties file.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | filegroups                             | ``-``                 | Specifies the group name of a collection file directory. Group names are separated by spaces.                                                                                                                                                                |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | filegroups.<filegroupName>.parentDir   | ``-``                 | Specifies the parent directory. The value must be an absolute path.                                                                                                                                                                                          |
      |                                        |                       |                                                                                                                                                                                                                                                              |
      |                                        |                       | This parameter can be set only in the properties.properties file.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | filegroups.<filegroupName>.filePattern | ``-``                 | Specifies the relative file path of the file group's parent directory. Directories can be included and regular expressions are supported. It must be used together with **parentDir**.                                                                       |
      |                                        |                       |                                                                                                                                                                                                                                                              |
      |                                        |                       | This parameter can be set only in the properties.properties file.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | positionFile                           | ``-``                 | Specifies the metadata storage path during data transmission.                                                                                                                                                                                                |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | headers.<filegroupName>.<headerKey>    | ``-``                 | Specifies the key-value of an event when data of a group is being collected.                                                                                                                                                                                 |
      |                                        |                       |                                                                                                                                                                                                                                                              |
      |                                        |                       | This parameter can be set only in the properties.properties file.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | byteOffsetHeader                       | false                 | Specifies whether each event header should contain the location information about the event in the source file. The location information is saved in the **byteoffset** variable.                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | skipToEnd                              | false                 | Specifies whether Flume can locate the latest location of a file and read the latest data after restart.                                                                                                                                                     |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | idleTimeout                            | 120000                | Specifies the idle duration during file reading, expressed in milliseconds. If the file data is not changed in this idle period, the source closes the file. If data is written into this file after it is closed, the source opens the file and reads data. |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | writePosInterval                       | 3000                  | Specifies the interval for writing metadata to a file, expressed in milliseconds.                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | batchSize                              | 1000                  | Specifies the number of events written to the channel in batches.                                                                                                                                                                                            |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime                                | 0 (Disabled)          | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the source is restarted. Unit: second                                                                                                                                 |
      +----------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Http Source**

   An HTTP source receives data from an external HTTP client and sends the data to the configured channels. :ref:`Table 5 <mrs_01_0396__en-us_topic_0000001173949378_t033eef1276424185b1cfd10a7d4e024f>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_t033eef1276424185b1cfd10a7d4e024f:

   .. table:: **Table 5** Common configurations of an HTTP source

      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Default Value                            | Description                                                                                                                                           |
      +=======================+==========================================+=======================================================================================================================================================+
      | channels              | ``-``                                    | Specifies the channel connected to the source. Multiple channels can be configured. This parameter can be set only in the properties.properties file. |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                  | http                                     | Specifies the type, which is set to **http**. This parameter can be set only in the properties.properties file.                                       |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | bind                  | ``-``                                    | Specifies the name or IP address of the bound host.                                                                                                   |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | port                  | ``-``                                    | Specifies the bound port.                                                                                                                             |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | handler               | org.apache.flume.source.http.JSONHandler | Specifies the message parsing method of an HTTP request. The following methods are supported:                                                         |
      |                       |                                          |                                                                                                                                                       |
      |                       |                                          | -  **org.apache.flume.source.http.JSONHandler**: JSON                                                                                                 |
      |                       |                                          | -  **org.apache.flume.sink.solr.morphline.BlobHandler**: BLOB                                                                                         |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | handler.\*            | ``-``                                    | Specifies handler parameters.                                                                                                                         |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | enableSSL             | false                                    | Specifies whether SSL is enabled in HTTP.                                                                                                             |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keystore              | ``-``                                    | Specifies the keystore path set after SSL is enabled in HTTP.                                                                                         |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | keystorePassword      | ``-``                                    | Specifies the keystore password set after SSL is enabled in HTTP.                                                                                     |
      +-----------------------+------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

Common Channel Configurations
-----------------------------

-  **Memory Channel**

   A memory channel uses memory as the cache. Events are stored in memory queues. :ref:`Table 6 <mrs_01_0396__en-us_topic_0000001173949378_tc1421df5bc6c415ca490e671ea935f85>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_tc1421df5bc6c415ca490e671ea935f85:

   .. table:: **Table 6** Common configurations of a memory channel

      +---------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
      | Parameter           | Default Value | Description                                                                                                       |
      +=====================+===============+===================================================================================================================+
      | type                | ``-``         | Specifies the type, which is set to **memory**. This parameter can be set only in the properties.properties file. |
      +---------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
      | capacity            | 10000         | Specifies the maximum number of events cached in a channel.                                                       |
      +---------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
      | transactionCapacity | 1000          | Specifies the maximum number of events accessed each time.                                                        |
      +---------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
      | channelfullcount    | 10            | Specifies the channel full count. When the count reaches the threshold, an alarm is reported.                     |
      +---------------------+---------------+-------------------------------------------------------------------------------------------------------------------+

-  **File Channel**

   A file channel uses local disks as the cache. Events are stored in the folder specified by **dataDirs**. :ref:`Table 7 <mrs_01_0396__en-us_topic_0000001173949378_td180d6190e86420d8779010b90877938>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_td180d6190e86420d8779010b90877938:

   .. table:: **Table 7** Common configurations of a file channel

      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter            | Default Value                         | Description                                                                                                                                     |
      +======================+=======================================+=================================================================================================================================================+
      | type                 | ``-``                                 | Specifies the type, which is set to **file**. This parameter can be set only in the properties.properties file.                                 |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | checkpointDir        | ${BIGDATA_DATA_HOME}/flume/checkpoint | Specifies the checkpoint storage directory.                                                                                                     |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | dataDirs             | ${BIGDATA_DATA_HOME}/flume/data       | Specifies the data cache directory. Multiple directories can be configured to improve performance. The directories are separated by commas (,). |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | maxFileSize          | 2146435071                            | Specifies the maximum size of a single cache file, expressed in bytes.                                                                          |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | minimumRequiredSpace | 524288000                             | Specifies the minimum idle space in the cache, expressed in bytes.                                                                              |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | capacity             | 1000000                               | Specifies the maximum number of events cached in a channel.                                                                                     |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | transactionCapacity  | 10000                                 | Specifies the maximum number of events accessed each time.                                                                                      |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | channelfullcount     | 10                                    | Specifies the channel full count. When the count reaches the threshold, an alarm is reported.                                                   |
      +----------------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Kafka Channel**

   A Kafka channel uses a Kafka cluster as the cache. Kafka provides high availability and multiple copies to prevent data from being immediately consumed by sinks when Flume or Kafka Broker crashes. :ref:`Table 10 Common configurations of a Kafka channel <mrs_01_0396__en-us_topic_0000001173949378_ta58e4ea5e98446418e498b81cf0c75b7>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_ta58e4ea5e98446418e498b81cf0c75b7:

   .. table:: **Table 8** Common configurations of a Kafka channel

      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | Parameter                        | Default Value         | Description                                                                                                     |
      +==================================+=======================+=================================================================================================================+
      | type                             | ``-``                 | Specifies the type, which is set to **org.apache.flume.channel.kafka.KafkaChannel**.                            |
      |                                  |                       |                                                                                                                 |
      |                                  |                       | This parameter can be set only in the properties.properties file.                                               |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.bootstrap.servers          | ``-``                 | Specifies the list of Brokers in the Kafka cluster.                                                             |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.topic                      | flume-channel         | Specifies the Kafka topic used by the channel to cache data.                                                    |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.consumer.group.id          | flume                 | Specifies the Kafka consumer group ID.                                                                          |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | parseAsFlumeEvent                | true                  | Specifies whether data is parsed into Flume events.                                                             |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | migrateZookeeperOffsets          | true                  | Specifies whether to search for offsets in ZooKeeper and submit them to Kafka when there is no offset in Kafka. |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.consumer.auto.offset.reset | latest                | Consumes data from the specified location when there is no offset.                                              |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.producer.security.protocol | SASL_PLAINTEXT        | Specifies the Kafka producer security protocol.                                                                 |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+
      | kafka.consumer.security.protocol | SASL_PLAINTEXT        | Specifies the Kafka consumer security protocol.                                                                 |
      +----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------+

Common Sink Configurations
--------------------------

-  **HDFS Sink**

   An HDFS sink writes data into HDFS. :ref:`Table 9 <mrs_01_0396__en-us_topic_0000001173949378_t3f4509459f734167afdd0cb20857d2ef>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_t3f4509459f734167afdd0cb20857d2ef:

   .. table:: **Table 9** Common configurations of an HDFS sink

      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                | Default Value         | Description                                                                                                                                                                                                                                         |
      +==========================+=======================+=====================================================================================================================================================================================================================================================+
      | channel                  | **-**                 | Specifies the channel connected to the sink. This parameter can be set only in the properties.properties file.                                                                                                                                      |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                     | hdfs                  | Specifies the type, which is set to **hdfs**. This parameter can be set only in the properties.properties file.                                                                                                                                     |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime                  | 0 (Disabled)          | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the sink is restarted. Unit: second                                                                                                                          |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.path                | ``-``                 | Specifies the HDFS path.                                                                                                                                                                                                                            |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.inUseSuffix         | .tmp                  | Specifies the suffix of the HDFS file to which data is being written.                                                                                                                                                                               |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.rollInterval        | 30                    | Specifies the interval for file rolling, expressed in seconds.                                                                                                                                                                                      |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.rollSize            | 1024                  | Specifies the size for file rolling, expressed in bytes.                                                                                                                                                                                            |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.rollCount           | 10                    | Specifies the number of events for file rolling.                                                                                                                                                                                                    |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.idleTimeout         | 0                     | Specifies the timeout interval for closing idle files automatically, expressed in seconds.                                                                                                                                                          |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.batchSize           | 1000                  | Specifies the number of events written into HDFS at a time.                                                                                                                                                                                         |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.kerberosPrincipal   | ``-``                 | Specifies the Kerberos username for HDFS authentication. This parameter is not required for a cluster in which Kerberos authentication is disabled.                                                                                                 |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.kerberosKeytab      | ``-``                 | Specifies the Kerberos keytab of HDFS authentication. This parameter is not required for a cluster in which Kerberos authentication is disabled.                                                                                                    |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.fileCloseByEndEvent | true                  | Specifies whether to close the file when the last event is received.                                                                                                                                                                                |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | hdfs.batchCallTimeout    | ``-``                 | Specifies the timeout control duration each time events are written into HDFS, expressed in milliseconds.                                                                                                                                           |
      |                          |                       |                                                                                                                                                                                                                                                     |
      |                          |                       | If this parameter is not specified, the timeout duration is controlled when each event is written into HDFS. When the value of **hdfs.batchSize** is greater than 0, configure this parameter to improve the performance of writing data into HDFS. |
      |                          |                       |                                                                                                                                                                                                                                                     |
      |                          |                       | .. note::                                                                                                                                                                                                                                           |
      |                          |                       |                                                                                                                                                                                                                                                     |
      |                          |                       |    The value of **hdfs.batchCallTimeout** depends on **hdfs.batchSize**. A greater **hdfs.batchSize** requires a larger **hdfs.batchCallTimeout**. If the value of **hdfs.batchCallTimeout** is too small, writing events to HDFS may fail.         |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | serializer.appendNewline | true                  | Specifies whether to add a line feed character (**\\n**) after an event is written to HDFS. If a line feed character is added, the data volume counters used by the line feed character will not be calculated by HDFS sinks.                       |
      +--------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Avro Sink**

   An Avro sink converts events into Avro events and sends them to the monitoring ports of the hosts. :ref:`Table 10 <mrs_01_0396__en-us_topic_0000001173949378_tcf9863ee677d41a6882b71987541fa33>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_tcf9863ee677d41a6882b71987541fa33:

   .. table:: **Table 10** Common configurations of an Avro sink

      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | Parameter           | Default Value | Description                                                                                                     |
      +=====================+===============+=================================================================================================================+
      | channel             | **-**         | Specifies the channel connected to the sink. This parameter can be set only in the properties.properties file.  |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | type                | ``-``         | Specifies the type, which is set to **avro**. This parameter can be set only in the properties.properties file. |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | hostname            | ``-``         | Specifies the name or IP address of the bound host.                                                             |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | port                | ``-``         | Specifies the monitoring port.                                                                                  |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | batch-size          | 1000          | Specifies the number of events sent in a batch.                                                                 |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | ssl                 | false         | Specifies whether to use SSL encryption.                                                                        |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | truststore-type     | JKS           | Specifies the Java trust store type.                                                                            |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | truststore          | ``-``         | Specifies the Java trust store file.                                                                            |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | truststore-password | ``-``         | Specifies the Java trust store password.                                                                        |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | keystore-type       | JKS           | Specifies the key storage type.                                                                                 |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | keystore            | ``-``         | Specifies the key storage file.                                                                                 |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+
      | keystore-password   | ``-``         | Specifies the key storage password.                                                                             |
      +---------------------+---------------+-----------------------------------------------------------------------------------------------------------------+

-  **HBase Sink**

   An HBase sink writes data into HBase. :ref:`Table 11 <mrs_01_0396__en-us_topic_0000001173949378_tf429beac69444e93a744abfe1d0fb744>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_tf429beac69444e93a744abfe1d0fb744:

   .. table:: **Table 11** Common configurations of an HBase sink

      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Default Value | Description                                                                                                                                          |
      +===================+===============+======================================================================================================================================================+
      | channel           | **-**         | Specifies the channel connected to the sink. This parameter can be set only in the properties.properties file.                                       |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type              | ``-``         | Specifies the type, which is set to **hbase**. This parameter can be set only in the properties.properties file.                                     |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | table             | ``-``         | Specifies the HBase table name.                                                                                                                      |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime           | 0 (Disabled)  | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the sink is restarted. Unit: second                           |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | columnFamily      | ``-``         | Specifies the HBase column family.                                                                                                                   |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | batchSize         | 1000          | Specifies the number of events written into HBase at a time.                                                                                         |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kerberosPrincipal | ``-``         | Specifies the Kerberos username for HBase authentication. This parameter is not required for a cluster in which Kerberos authentication is disabled. |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kerberosKeytab    | ``-``         | Specifies the Kerberos keytab of HBase authentication. This parameter is not required for a cluster in which Kerberos authentication is disabled.    |
      +-------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Kafka Sink**

   A Kafka sink writes data into Kafka. :ref:`Table 12 <mrs_01_0396__en-us_topic_0000001173949378_tf898876f2a2f45629655554005c3f0a8>` lists common configurations.

   .. _mrs_01_0396__en-us_topic_0000001173949378_tf898876f2a2f45629655554005c3f0a8:

   .. table:: **Table 12** Common configurations of a Kafka sink

      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                       | Default Value         | Description                                                                                                                                                                       |
      +=================================+=======================+===================================================================================================================================================================================+
      | channel                         | **-**                 | Specifies the channel connected to the sink. This parameter can be set only in the properties.properties file.                                                                    |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                            | ``-``                 | Specifies the type, which is set to **org.apache.flume.sink.kafka.KafkaSink**.                                                                                                    |
      |                                 |                       |                                                                                                                                                                                   |
      |                                 |                       | This parameter can be set only in the properties.properties file.                                                                                                                 |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.bootstrap.servers         | ``-``                 | Specifies the list of Kafka Brokers, which are separated by commas.                                                                                                               |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | monTime                         | 0 (Disabled)          | Specifies the thread monitoring threshold. When the update time exceeds the threshold, the sink is restarted. Unit: second                                                        |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.topic                     | default-flume-topic   | Specifies the topic where data is written.                                                                                                                                        |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | flumeBatchSize                  | 1000                  | Specifies the number of events written into Kafka at a time.                                                                                                                      |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.security.protocol         | SASL_PLAINTEXT        | Specifies the security protocol of Kafka. The value must be set to **PLAINTEXT** for clusters in which Kerberos authentication is disabled.                                       |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | kafka.kerberos.domain.name      | ``-``                 | Specifies the Kafka domain name. This parameter is mandatory for a security cluster. This parameter can be set only in the properties.properties file.                            |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Other Kafka Producer Properties | ``-``                 | Specifies other Kafka configurations. This parameter can be set to any production configuration supported by Kafka, and the **.kafka** prefix must be added to the configuration. |
      |                                 |                       |                                                                                                                                                                                   |
      |                                 |                       | This parameter can be set only in the properties.properties file.                                                                                                                 |
      +---------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
