:original_name: mrs_01_1063.html

.. _mrs_01_1063:

Typical Scenario: Collecting Local Static Logs and Uploading Them to HDFS
=========================================================================

Scenario
--------

This section describes how to use Flume client to collect static logs from a local PC and save them to the **/flume/test** directory on HDFS.

.. note::

   By default, the cluster network environment is secure and the SSL authentication is not enabled during the data transmission process. For details about how to use the encryption mode, see :ref:`Configuring the Encrypted Transmission <mrs_01_1069>`. The configuration applies to scenarios where only the Flume is configured, for example, Spooldir Source+Memory Channel+HDFS Sink.

Prerequisites
-------------

-  The cluster, HDFS, and Flume service have been installed.
-  The Flume client has been installed. For details about how to install the client, see :ref:`Installing the Flume Client on Clusters <mrs_01_1595>`.
-  The network environment of the cluster is secure.
-  User **flume_hdfs** has been created, and the HDFS directory and data used for log verification have been authorized to the user.

Procedure
---------

#. On FusionInsight Manager, choose **System** > **Permission > User**, select user **flume_hdfs**, and choose **More** > **Download Authentication Credential** to download the Kerberos certificate file of user **flume_hdfs** and save it to the local host.

#. Set Flume parameters.

   Use Flume on FusionInsight Manager to configure the Flume role client parameters and generate a configuration file.

   a. Log in to FusionInsight Manager. Choose **Cluster** > **Services** > **Flume** > **Configuration Tool**.

   b. Set **Agent Name** to **client**. Select the source, channel, and sink to be used, drag them to the GUI on the right, and connect them.

      Use SpoolDir Source, Memory Channel, and HDFS Sink.


      .. figure:: /_static/images/en-us_image_0000001295900052.png
         :alt: **Figure 1** Example for the Flume configuration tool

         **Figure 1** Example for the Flume configuration tool

   c. Double-click the source, channel, and sink. Set corresponding configuration parameters by referring to :ref:`Table 1 <mrs_01_1063__t3a5e921315234eb6a22b607e40f19e8a>` based on the actual environment.

      .. note::

         -  If you want to continue using the **properties.propretites** file by modifying it, log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services**. On the page that is displayed, choose **Flume**. On the displayed page, click the **Configuration Tool** tab, click **Import**, import the file, and modify the configuration items related to non-encrypted transmission.
         -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.

   d. .. _mrs_01_1063__ld87a5f43900a41ad8cda390510028ae7:

      Click **Export** to save the **properties.properties** configuration file to the local.

      .. _mrs_01_1063__t3a5e921315234eb6a22b607e40f19e8a:

      .. table:: **Table 1** Parameters to be modified of the Flume role client

         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter              | Description                                                                                                                                                                                                    | Example Value                                                                                                                                                                                                                              |
         +========================+================================================================================================================================================================================================================+============================================================================================================================================================================================================================================+
         | Name                   | The value must be unique and cannot be left blank.                                                                                                                                                             | test                                                                                                                                                                                                                                       |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | spoolDir               | Specifies the directory where the file to be collected resides. This parameter cannot be left blank. The directory needs to exist and have the write, read, and execute permissions on the flume running user. | /srv/BigData/hadoop/data1/zb                                                                                                                                                                                                               |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | trackerDir             | Specifies the path for storing the metadata of files collected by Flume.                                                                                                                                       | /srv/BigData/hadoop/data1/tracker                                                                                                                                                                                                          |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | batch-size             | Specifies the number of events that Flume sends in a batch.                                                                                                                                                    | 61200                                                                                                                                                                                                                                      |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.path              | Specifies the HDFS data write directory. This parameter cannot be left blank.                                                                                                                                  | hdfs://hacluster/flume/test                                                                                                                                                                                                                |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.inUsePrefix       | Specifies the prefix of the file that is being written to HDFS.                                                                                                                                                | TMP\_                                                                                                                                                                                                                                      |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.batchSize         | Specifies the maximum number of events that can be written to HDFS once.                                                                                                                                       | 61200                                                                                                                                                                                                                                      |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.kerberosPrincipal | Specifies the Kerberos authentication user, which is mandatory in security versions. This configuration is required only in security clusters.                                                                 | flume_hdfs                                                                                                                                                                                                                                 |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.kerberosKeytab    | Specifies the keytab file path for Kerberos authentication, which is mandatory in security versions. This configuration is required only in security clusters.                                                 | /opt/test/conf/user.keytab                                                                                                                                                                                                                 |
         |                        |                                                                                                                                                                                                                |                                                                                                                                                                                                                                            |
         |                        |                                                                                                                                                                                                                | .. note::                                                                                                                                                                                                                                  |
         |                        |                                                                                                                                                                                                                |                                                                                                                                                                                                                                            |
         |                        |                                                                                                                                                                                                                |    Obtain the **user.keytab** file from the Kerberos certificate file of the user **flume_hdfs**. In addition, ensure that the user who installs and runs the Flume client has the read and write permissions on the **user.keytab** file. |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hdfs.useLocalTimeStamp | Specifies whether to use the local time. Possible values are **true** and **false**.                                                                                                                           | true                                                                                                                                                                                                                                       |
         +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Upload the configuration file.

   Upload the file exported in :ref:`2.d <mrs_01_1063__ld87a5f43900a41ad8cda390510028ae7>` to the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf** directory of the cluster

4. Verify log transmission.

   a. Log in to FusionInsight Manager as a user who has the management permission on HDFS. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **HDFS**. On the page that is displayed, click the **NameNode(**\ *Node name*\ **,Active)** link next to **NameNode WebUI** to go to the HDFS web UI. On the displayed page, choose **Utilities** > **Browse the file system**.

   b. Check whether the data is generated in the **/flume/test** directory on the HDFS.


      .. figure:: /_static/images/en-us_image_0000001296059892.png
         :alt: **Figure 2** Checking HDFS directories and files

         **Figure 2** Checking HDFS directories and files
