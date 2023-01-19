:original_name: mrs_01_1065.html

.. _mrs_01_1065:

Typical Scenario: Collecting Logs from Kafka and Uploading Them to HDFS
=======================================================================

Scenario
--------

This section describes how to use Flume client to collect logs from the Topic list (test1) of Kafka and save them to the **/flume/test** directory on HDFS.

.. note::

   By default, the cluster network environment is secure and the SSL authentication is not enabled during the data transmission process. For details about how to use the encryption mode, see :ref:`Configuring the Encrypted Transmission <mrs_01_1069>`. The configuration applies to scenarios where only the Flume is configured, for example, Kafka Source+Memory Channel+HDFS Sink.

Prerequisites
-------------

-  The cluster, HDFS, Kafka, and Flume service have been installed.
-  The Flume client has been installed. For details about how to install the client, see :ref:`Installing the Flume Client on Clusters <mrs_01_1595>`.
-  The network environment of the cluster is secure.
-  You have created user **flume_hdfs** and authorized the HDFS directory and data to be operated during log verification. For details, see :ref:`Adding a Ranger Access Permission Policy for HDFS <mrs_01_1856>`.

Procedure
---------

#. On FusionInsight Manager, choose **System > User** and choose **More > Download Authentication Credential** to download the Kerberos certificate file of user **flume_hdfs** and save it to the local host.

#. Configure the client parameters of the Flume role.

   Use the Flume configuration tool on FusionInsight Manager to configure the Flume role client parameters and generate a configuration file.

   a. Log in to FusionInsight Manager and choose **Cluster** > **Services**. On the page that is displayed, choose **Flume**. On the displayed page, click the **Configuration Tool** tab.

   b. Set **Agent Name** to **client**. Select the source, channel, and sink to be used, drag them to the GUI on the right, and connect them.

      For example, use Kafka Source, Memory Channel, and HDFS Sink.


      .. figure:: /_static/images/en-us_image_0000001295740052.png
         :alt: **Figure 1** Example for the Flume configuration tool

         **Figure 1** Example for the Flume configuration tool

   c. Double-click the source, channel, and sink. Set corresponding configuration parameters by seeing :ref:`Table 1 <mrs_01_1065__t6c3b4afafa084081b9b2d9400d6ea379>` based on the actual environment.

      .. note::

         -  If you want to continue using the **properties.propretites** file by modifying it, log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services**. On the page that is displayed, choose **Flume**. On the displayed page, click the **Configuration Tool** tab, click **Import**, import the file, and modify the configuration items related to non-encrypted transmission.
         -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.

   d. .. _mrs_01_1065__l92b924df515f493daa8ec019ca9fcec4:

      Click **Export** to save the **properties.properties** configuration file to the local.

      .. _mrs_01_1065__t6c3b4afafa084081b9b2d9400d6ea379:

      .. table:: **Table 1** Parameters to be modified of the Flume role client

         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter               | Description                                                                                                                                                                                                                                     | Example Value                                                                                                                                                                                                                              |
         +=========================+=================================================================================================================================================================================================================================================+============================================================================================================================================================================================================================================+
         | Name                    | The value must be unique and cannot be left blank.                                                                                                                                                                                              | test                                                                                                                                                                                                                                       |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | kafka.topics            | Specifies the subscribed Kafka topic list, in which topics are separated by commas (,). This parameter cannot be left blank.                                                                                                                    | test1                                                                                                                                                                                                                                      |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | kafka.consumer.group.id | Specifies the data group ID obtained from Kafka. This parameter cannot be left blank.                                                                                                                                                           | flume                                                                                                                                                                                                                                      |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | kafka.bootstrap.servers | Specifies the bootstrap IP address and port list of Kafka. The default value is all Kafka lists in a Kafka cluster. If Kafka has been installed in the cluster and its configurations have been synchronized, this parameter can be left blank. | 192.168.101.10:9092                                                                                                                                                                                                                        |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | batchSize               | Specifies the number of events that Flume sends in a batch (number of data pieces).                                                                                                                                                             | 61200                                                                                                                                                                                                                                      |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.path               | Specifies the HDFS data write directory. This parameter cannot be left blank.                                                                                                                                                                   | hdfs://hacluster/flume/test                                                                                                                                                                                                                |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.inUsePrefix        | Specifies the prefix of the file that is being written to HDFS.                                                                                                                                                                                 | TMP\_                                                                                                                                                                                                                                      |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.batchSize          | Specifies the maximum number of events that can be written to HDFS once.                                                                                                                                                                        | 61200                                                                                                                                                                                                                                      |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.kerberosPrincipal  | Specifies the Kerberos authentication user, which is mandatory in security versions. This configuration is required only in security clusters.                                                                                                  | flume_hdfs                                                                                                                                                                                                                                 |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.kerberosKeytab     | Specifies the keytab file path for Kerberos authentication, which is mandatory in security versions. This configuration is required only in security clusters.                                                                                  | /opt/test/conf/user.keytab                                                                                                                                                                                                                 |
         |                         |                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                            |
         |                         |                                                                                                                                                                                                                                                 | .. note::                                                                                                                                                                                                                                  |
         |                         |                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                            |
         |                         |                                                                                                                                                                                                                                                 |    Obtain the **user.keytab** file from the Kerberos certificate file of the user **flume_hdfs**. In addition, ensure that the user who installs and runs the Flume client has the read and write permissions on the **user.keytab** file. |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.useLocalTimeStamp  | Specifies whether to use the local time. Possible values are **true** and **false**.                                                                                                                                                            | true                                                                                                                                                                                                                                       |
         +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Upload the configuration file.

   Upload the file exported in :ref:`2.d <mrs_01_1065__l92b924df515f493daa8ec019ca9fcec4>` to the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf** directory of the cluster

4. Verify log transmission.

   a. Log in to FusionInsight Manager as a user who has the management permission on HDFS. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **HDFS**. On the page that is displayed, click the **NameNode(**\ *Node name*\ **,Active)** link next to **NameNode WebUI** to go to the HDFS web UI. On the displayed page, choose **Utilities** > **Browse the file system**.

   b. Check whether the data is generated in the **/flume/test** directory on the HDFS.


      .. figure:: /_static/images/en-us_image_0000001349059705.png
         :alt: **Figure 2** Checking HDFS directories and files

         **Figure 2** Checking HDFS directories and files
