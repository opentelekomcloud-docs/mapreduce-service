:original_name: mrs_01_1580.html

.. _mrs_01_1580:

Configuring Kafka
=================

Sample project data of Flink is stored in Kafka. A user with Kafka permission can send data to Kafka and receive data from it.

#. Ensure that clusters, including HDFS, Yarn, Flink, and Kafka are installed.

#. Create a topic.

   -  Run Linux command line to create a topic. Before running commands, ensure that the kinit command, for example, **kinit flinkuser**, is run for authentication.

      .. note::

         To create a Flink user, you need to have the permission to create Kafka topics.

      The format of the command is shown as follows, in which **{zkQuorum}** indicates ZooKeeper cluster information and the format is *IP*:*port*, and **{Topic}** indicates the topic name.

      **bin/kafka-topics.sh --create --zookeeper {zkQuorum}/kafka --replication-factor 1 --partitions 5 --topic {Topic}**

      Assume the topic name is **topic 1**. The command for creating this topic is displayed as follows:

      .. code-block::

         /opt/client/Kafka/kafka/bin/kafka-topics.sh --create --zookeeper 10.96.101.32:2181,10.96.101.251:2181,10.96.101.177:2181,10.91.8.160:2181/kafka --replication-factor 1 --partitions 5 --topic topic1

   -  Configure the permission of the topic on the server.

      Set the **allow.everyone.if.no.acl.found** parameter of Kafka Broker to **true**.

#. Perform the security authentication.

   The Kerberos authentication, SSL encryption authentication, or Kerberos + SSL authentication mode can be used.

   .. note::

      For versions earlier than MRS 3.x, only Kerberos authentication is supported.

   -  **Kerberos authentication**

      -  Client configuration

         In the Flink configuration file **flink-conf.yaml**, add configurations about Kerberos authentication. For example, add **KafkaClient** in **contexts** as follows:

         .. code-block::

            security.kerberos.login.keytab: /home/demo/keytab/flinkuser.keytab
            security.kerberos.login.principal: flinkuser
            security.kerberos.login.contexts: Client,KafkaClient
            security.kerberos.login.use-ticket-cache: false

         .. note::

            For versions earlier than MRS 3.x, set **security.kerberos.login.keytab** to **/home/demo/flink/release/keytab/flinkuser.keytab**.

      -  Running parameter

         Running parameters about the **SASL_PLAINTEXT** protocol are as follows:

         .. code-block::

            --topic topic1 --bootstrap.servers 10.96.101.32:21007 --security.protocol SASL_PLAINTEXT  --sasl.kerberos.service.name kafka //10.96.101.32:21007 indicates the IP:port of the Kafka server.

   -  **SSL encryption**

      -  Configure the server.

         Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Kafka** > **Configurations**, and set **Type** to **All**. Search for **ssl.mode.enable** and set it to **true**.

      -  Configure the client.

         a. Log in to FusionInsight Manager, choose **Cluster > Name of the desired cluster > Services > Kafka > More > Download Client** to download Kafka client.

         b. Use the **ca.crt** certificate file in the client root directory to generate the **truststore** file for the client.

            Run the following command:

            .. code-block::

               keytool -noprompt -import -alias myservercert -file ca.crt -keystore truststore.jks

            The command execution result is similar to the following:

            |image1|

         c. Run parameters.

            The value of **ssl.truststore.password** must be the same as the password you entered when creating **truststore**. Run the following command to run parameters:

            .. code-block::

               --topic topic1 --bootstrap.servers 10.96.101.32:9093 --security.protocol SSL --ssl.truststore.location /home/zgd/software/FusionInsight_Kafka_ClientConfig/truststore.jks --ssl.truststore.password XXX

   -  **Kerberos+SSL** **encryption**

      After completing preceding configurations of the client and server of Kerberos and SSL, modify the port number and protocol type in running parameters to enable the Kerberos+SSL encryption mode.

      .. code-block::

         --topic topic1 --bootstrap.servers 10.96.101.32:21009 --security.protocol SASL_SSL  --sasl.kerberos.service.name kafka --ssl.truststore.location /home/zgd/software/FusionInsight_Kafka_ClientConfig/truststore.jks --ssl.truststore.password XXX

.. |image1| image:: /_static/images/en-us_image_0000001295930604.png
