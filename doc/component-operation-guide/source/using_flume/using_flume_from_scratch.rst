:original_name: mrs_01_0397.html

.. _mrs_01_0397:

Using Flume from Scratch
========================

Scenario
--------

You can use Flume to import collected log information to Kafka.

Prerequisites
-------------

-  A streaming cluster that contains components such as Flume and Kafka and has Kerberos authentication enabled has been created.
-  The streaming cluster can properly communicate with the node where logs are generated.

Using the Flume Client (Versions Earlier Than MRS 3.x)
------------------------------------------------------

.. note::

   You do not need to perform :ref:`2 <mrs_01_0397__l78730912572649fd8edfda3920dc20cf>` to :ref:`6 <mrs_01_0397__lfde322e0f3de4ccb88b4e195e65f9993>` for a normal cluster.

#. Install the Flume client.

   Install the Flume client in a directory, for example, **/opt/Flumeclient**, on the node where logs are generated by referring to :ref:`Installing the Flume Client on Clusters of Versions Earlier Than MRS 3.x <mrs_01_1594>`. The Flume client installation directories in the following steps are only examples. Change them to the actual installation directories.

#. .. _mrs_01_0397__l78730912572649fd8edfda3920dc20cf:

   Copy the configuration file of the authentication server from the Master1 node to the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf** directory on the node where the Flume client is installed.

   For versions earlier than MRS 1.9.2, **${BIGDATA_HOME}/FusionInsight/etc/1\_**\ *X*\ **\_KerberosClient/kdc.conf** is used as the full file path.

   For versions earlier than MRS 3.\ *x*, **${BIGDATA_HOME}/MRS_Current/1\_**\ *X*\ **\_KerberosClient/etc/kdc.conf** is used as the full file path.

   In the preceding paths, **X** indicates a random number. Change it based on the site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. Check the service IP address of any node where the Flume role is deployed.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager. Choose **Cluster** > **Services** > **Flume** > **Instance**. Query **Service IP Address** of any node on which the Flume role is deployed.
   -  For MRS 1.9.2 to versions earlier than 3.x, click the cluster name on the MRS console and choose *Name of the desired cluster* > **Components** > **Flume** > **Instances** to view **Business IP Address** of any node where the Flume role is deployed.

#. .. _mrs_01_0397__l762ab29694a642ac8ae1a0609cb97c9b:

   Copy the user authentication file from this node to the *Flume client installation directory*\ **/fusioninsight-flume-Flume component version number/conf** directory on the Flume client node.

   For versions earlier than MRS 1.9.2, **${BIGDATA_HOME}/FusionInsight/FusionInsight-Flume-**\ *Flume component version number*\ **/flume/conf/flume.keytab** is used as the full file path.

   For versions earlier than 3.\ *x*, **${BIGDATA_HOME}/MRS\_**\ *XXX*\ **/install/FusionInsight-Flume-**\ *Flume component version number*\ **/flume/conf/flume.keytab** is used as the full file path.

   In the preceding paths, **XXX** indicates the product version number. Change it based on the site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. Copy the **jaas.conf** file from this node to the **conf** directory on the Flume client node.

   For versions earlier than MRS 1.9.2, **${BIGDATA_HOME}/FusionInsight/etc/1\_**\ *X*\ **\_Flume/jaas.conf** is used as the full file path.

   For versions earlier than MRS 3.\ *x*, **${BIGDATA_HOME}/MRS_Current/1\_**\ *X*\ **\_Flume/etc/jaas.conf** is used as the full file path.

   In the preceding path, **X** indicates a random number. Change it based on the site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. .. _mrs_01_0397__lfde322e0f3de4ccb88b4e195e65f9993:

   Log in to the Flume client node and go to the client installation directory. Run the following command to modify the file:

   **vi conf/jaas.conf**

   Change the full path of the user authentication file defined by **keyTab** to the **Flume client installation directory/fusioninsight-flume-*Flume component version number*/conf** saved in :ref:`4 <mrs_01_0397__l762ab29694a642ac8ae1a0609cb97c9b>`, and save the modification and exit.

#. Run the following command to modify the **flume-env.sh** configuration file of the Flume client:

   **vi** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf/flume-env.sh**

   Add the following information after **-XX:+UseCMSCompactAtFullCollection**:

   .. code-block::

      -Djava.security.krb5.conf=Flume client installation directory/fusioninsight-flume-1.9.0/conf/kdc.conf -Djava.security.auth.login.config=Flume client installation directory/fusioninsight-flume-1.9.0/conf/jaas.conf -Dzookeeper.request.timeout=120000

   Example: **"-XX:+UseCMSCompactAtFullCollection -Djava.security.krb5.conf=/opt/FlumeClient**/**fusioninsight-flume-**\ *Flume component version number*\ **/conf/kdc.conf -Djava.security.auth.login.config=/opt/FlumeClient**/**fusioninsight-flume-**\ *Flume component version number*\ **/conf/jaas.conf -Dzookeeper.request.timeout=120000"**

   Change *Flume client installation directory* to the actual installation directory. Then save and exit.

#. Run the following command to restart the Flume client:

   **cd** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/bin**

   **./flume-manage.sh restart**

   Example:

   **cd /opt/FlumeClient/fusioninsight-flume-**\ *Flume component version number*\ **/bin**

   **./flume-manage.sh restart**

#. Run the following command to configure and save jobs in the Flume client configuration file **properties.properties** based on service requirements.

   **vi** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf/properties.properties**

   The following uses SpoolDir Source+File Channel+Kafka Sink as an example:

   .. code-block::

      #########################################################################################
      client.sources = static_log_source
      client.channels = static_log_channel
      client.sinks = kafka_sink
      #########################################################################################
      #LOG_TO_HDFS_ONLINE_1

      client.sources.static_log_source.type = spooldir
      client.sources.static_log_source.spoolDir = Monitoring directory
      client.sources.static_log_source.fileSuffix = .COMPLETED
      client.sources.static_log_source.ignorePattern = ^$
      client.sources.static_log_source.trackerDir = Metadata storage path during transmission
      client.sources.static_log_source.maxBlobLength = 16384
      client.sources.static_log_source.batchSize = 51200
      client.sources.static_log_source.inputCharset = UTF-8
      client.sources.static_log_source.deserializer = LINE
      client.sources.static_log_source.selector.type = replicating
      client.sources.static_log_source.fileHeaderKey = file
      client.sources.static_log_source.fileHeader = false
      client.sources.static_log_source.basenameHeader = true
      client.sources.static_log_source.basenameHeaderKey = basename
      client.sources.static_log_source.deletePolicy = never

      client.channels.static_log_channel.type = file
      client.channels.static_log_channel.dataDirs = Data cache path. Multiple paths, separated by commas (,), can be configured to improve performance.
      client.channels.static_log_channel.checkpointDir = Checkpoint storage path
      client.channels.static_log_channel.maxFileSize = 2146435071
      client.channels.static_log_channel.capacity = 1000000
      client.channels.static_log_channel.transactionCapacity = 612000
      client.channels.static_log_channel.minimumRequiredSpace = 524288000

      client.sinks.kafka_sink.type = org.apache.flume.sink.kafka.KafkaSink
      client.sinks.kafka_sink.kafka.topic = Topic to which data is written, for example, flume_test
      client.sinks.kafka_sink.kafka.bootstrap.servers = XXX.XXX.XXX.XXX:Kafka port number,XXX.XXX.XXX.XXX:Kafka port number,XXX.XXX.XXX.XXX:Kafka port number
      client.sinks.kafka_sink.flumeBatchSize = 1000
      client.sinks.kafka_sink.kafka.producer.type = sync
      client.sinks.kafka_sink.kafka.security.protocol = SASL_PLAINTEXT
      client.sinks.kafka_sink.kafka.kerberos.domain.name = Kafka domain name. This parameter is mandatory for a security cluster.
      client.sinks.kafka_sink.requiredAcks = 0

      client.sources.static_log_source.channels = static_log_channel
      client.sinks.kafka_sink.channel = static_log_channel

   .. note::

      -  **client.sinks.kafka_sink.kafka.topic**: Topic to which data is written. If the topic does not exist in Kafka, it is automatically created by default.

      -  **client.sinks.kafka_sink.kafka.bootstrap.servers**: List of Kafka Brokers, which are separated by commas (,). By default, the port is **21007** for a security cluster and **9092** for a normal cluster.

      -  **client.sinks.kafka_sink.kafka.security.protocol**: The value is **SASL_PLAINTEXT** for a security cluster and **PLAINTEXT** for a normal cluster.

      -  **client.sinks.kafka_sink.kafka.kerberos.domain.name**:

         You do not need to set this parameter for a normal cluster. For a security cluster, the value of this parameter is the value of **kerberos.domain.name** in the Kafka cluster.

         For versions earlier than MRS 1.9.2, obtain the value by checking **${BIGDATA_HOME}/FusionInsight/etc/1\_**\ *X*\ **\_Broker/server.properties** on the node where the broker instance resides.

         Obtain the value for versions earlier than MRS 3.\ *x* by checking **${BIGDATA_HOME}/MRS_Current/1\_**\ *X*\ **\_Broker/etc/server.properties** on the node where the broker instance resides.

         In the preceding paths, **X** indicates a random number. Change it based on site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. After the parameters are set and saved, the Flume client automatically loads the content configured in **properties.properties**. When new log files are generated by spoolDir, the files are sent to Kafka producers and can be consumed by Kafka consumers.

Using the Flume Client (MRS 3.x or Later)
-----------------------------------------

.. note::

   You do not need to perform :ref:`2 <mrs_01_0397__li81278495417>` to :ref:`6 <mrs_01_0397__li31329494415>` for a normal cluster.

#. Install the Flume client.

   Install the Flume client in a directory, for example, **/opt/Flumeclient**, on the node where logs are generated by referring to :ref:`Installing the Flume Client on MRS 3.x or Later Clusters <mrs_01_1595>`. The Flume client installation directories in the following steps are only examples. Change them to the actual installation directories.

#. .. _mrs_01_0397__li81278495417:

   Copy the configuration file of the authentication server from the Master1 node to the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf** directory on the node where the Flume client is installed.

   The full file path is **${BIGDATA_HOME}/FusionInsight\_**\ **BASE\_**\ *XXX*\ **/1\_**\ *X*\ **\_KerberosClient/etc/kdc.conf**. In the preceding path, **XXX** indicates the product version number. **X** indicates a random number. Replace them based on site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. Check the service IP address of any node where the Flume role is deployed.

   Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster > Services > Flume > Instance**. Check the service IP address of any node where the Flume role is deployed.

#. .. _mrs_01_0397__li4130849748:

   Copy the user authentication file from this node to the *Flume client installation directory*\ **/fusioninsight-flume-Flume component version number/conf** directory on the Flume client node.

   The full file path is **${BIGDATA_HOME}/FusionInsight_Porter\_**\ *XXX*\ **/install/FusionInsight-Flume-**\ *Flume component version number*\ **/flume/conf/flume.keytab**.

   In the preceding paths, **XXX** indicates the product version number. Change it based on the site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. Copy the **jaas.conf** file from this node to the **conf** directory on the Flume client node.

   The full file path is **${BIGDATA_HOME}/FusionInsight_Current/1\_**\ *X*\ **\_Flume/etc/jaas.conf**.

   In the preceding path, **X** indicates a random number. Change it based on the site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. .. _mrs_01_0397__li31329494415:

   Log in to the Flume client node and go to the client installation directory. Run the following command to modify the file:

   **vi conf/jaas.conf**

   Change the full path of the user authentication file defined by **keyTab** to the **Flume client installation directory/fusioninsight-flume-*Flume component version number*/conf** saved in :ref:`4 <mrs_01_0397__li4130849748>`, and save the modification and exit.

#. Run the following command to modify the **flume-env.sh** configuration file of the Flume client:

   **vi** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf/flume-env.sh**

   Add the following information after **-XX:+UseCMSCompactAtFullCollection**:

   .. code-block::

      -Djava.security.krb5.conf=Flume client installation directory/fusioninsight-flume-1.9.0/conf/kdc.conf -Djava.security.auth.login.config=Flume client installation directory/fusioninsight-flume-1.9.0/conf/jaas.conf -Dzookeeper.request.timeout=120000

   Example: **"-XX:+UseCMSCompactAtFullCollection -Djava.security.krb5.conf=/opt/FlumeClient**/**fusioninsight-flume-**\ *Flume component version number*\ **/conf/kdc.conf -Djava.security.auth.login.config=/opt/FlumeClient**/**fusioninsight-flume-**\ *Flume component version number*\ **/conf/jaas.conf -Dzookeeper.request.timeout=120000"**

   Change *Flume client installation directory* to the actual installation directory. Then save and exit.

#. Run the following command to restart the Flume client:

   **cd** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/bin**

   **./flume-manage.sh restart**

   Example:

   **cd /opt/FlumeClient/fusioninsight-flume-**\ *Flume component version number*\ **/bin**

   **./flume-manage.sh restart**

#. Configure jobs based on actual service scenarios.

   -  Some parameters, for MRS 3.\ *x* or later, can be configured on Manager.

   -  Set the parameters in the **properties.properties** file. The following uses SpoolDir Source+File Channel+Kafka Sink as an example.

      Run the following command on the node where the Flume client is installed. Configure and save jobs in the Flume client configuration file **properties.properties** based on actual service requirements.

      **vi** *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf/properties.properties**

      .. code-block::

         #########################################################################################
         client.sources = static_log_source
         client.channels = static_log_channel
         client.sinks = kafka_sink
         #########################################################################################
         #LOG_TO_HDFS_ONLINE_1

         client.sources.static_log_source.type = spooldir
         client.sources.static_log_source.spoolDir = Monitoring directory
         client.sources.static_log_source.fileSuffix = .COMPLETED
         client.sources.static_log_source.ignorePattern = ^$
         client.sources.static_log_source.trackerDir = Metadata storage path during transmission
         client.sources.static_log_source.maxBlobLength = 16384
         client.sources.static_log_source.batchSize = 51200
         client.sources.static_log_source.inputCharset = UTF-8
         client.sources.static_log_source.deserializer = LINE
         client.sources.static_log_source.selector.type = replicating
         client.sources.static_log_source.fileHeaderKey = file
         client.sources.static_log_source.fileHeader = false
         client.sources.static_log_source.basenameHeader = true
         client.sources.static_log_source.basenameHeaderKey = basename
         client.sources.static_log_source.deletePolicy = never

         client.channels.static_log_channel.type = file
         client.channels.static_log_channel.dataDirs = Data cache path. Multiple paths, separated by commas (,), can be configured to improve performance.
         client.channels.static_log_channel.checkpointDir = Checkpoint storage path
         client.channels.static_log_channel.maxFileSize = 2146435071
         client.channels.static_log_channel.capacity = 1000000
         client.channels.static_log_channel.transactionCapacity = 612000
         client.channels.static_log_channel.minimumRequiredSpace = 524288000

         client.sinks.kafka_sink.type = org.apache.flume.sink.kafka.KafkaSink
         client.sinks.kafka_sink.kafka.topic = Topic to which data is written, for example, flume_test
         client.sinks.kafka_sink.kafka.bootstrap.servers = XXX.XXX.XXX.XXX:Kafka port number,XXX.XXX.XXX.XXX:Kafka port number,XXX.XXX.XXX.XXX:Kafka port number
         client.sinks.kafka_sink.flumeBatchSize = 1000
         client.sinks.kafka_sink.kafka.producer.type = sync
         client.sinks.kafka_sink.kafka.security.protocol = SASL_PLAINTEXT
         client.sinks.kafka_sink.kafka.kerberos.domain.name = Kafka domain name. This parameter is mandatory for a security cluster.
         client.sinks.kafka_sink.requiredAcks = 0

         client.sources.static_log_source.channels = static_log_channel
         client.sinks.kafka_sink.channel = static_log_channel

      .. note::

         -  **client.sinks.kafka_sink.kafka.topic**: Topic to which data is written. If the topic does not exist in Kafka, it is automatically created by default.

         -  **client.sinks.kafka_sink.kafka.bootstrap.servers**: List of Kafka Brokers, which are separated by commas (,). By default, the port is **21007** for a security cluster and **9092** for a normal cluster.

         -  **client.sinks.kafka_sink.kafka.security.protocol**: The value is **SASL_PLAINTEXT** for a security cluster and **PLAINTEXT** for a normal cluster.

         -  **client.sinks.kafka_sink.kafka.kerberos.domain.name**:

            You do not need to set this parameter for a normal cluster. For a security cluster, the value of this parameter is the value of **kerberos.domain.name** in the Kafka cluster.

            For versions earlier than MRS 1.9.2, obtain the value by checking **${BIGDATA_HOME}/FusionInsight/etc/1\_**\ *X*\ **\_Broker/server.properties** on the node where the broker instance resides.

            Obtain the value for versions earlier than MRS 3.\ *x* by checking **${BIGDATA_HOME}/MRS_Current/1\_**\ *X*\ **\_Broker/etc/server.properties** on the node where the broker instance resides.

            In the preceding paths, **X** indicates a random number. Change it based on site requirements. The file must be saved by the user who installs the Flume client, for example, user **root**.

#. After the parameters are set and saved, the Flume client automatically loads the content configured in **properties.properties**. When new log files are generated by spoolDir, the files are sent to Kafka producers and can be consumed by Kafka consumers.
