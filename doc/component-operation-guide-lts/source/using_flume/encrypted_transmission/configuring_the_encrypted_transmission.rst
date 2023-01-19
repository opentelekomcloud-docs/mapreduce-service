:original_name: mrs_01_1069.html

.. _mrs_01_1069:

Configuring the Encrypted Transmission
======================================

Scenario
--------

This section describes how to configure the server and client parameters of the Flume service (including the Flume and MonitorServer roles) after the cluster is installed to ensure proper running of the service.

Prerequisites
-------------

The cluster and Flume service have been installed.

Procedure
---------

#. Generate the certificate trust lists of the server and client of the Flume role respectively.

   a. Remotely log in to the node using ECM where the Flume server is to be installed as user **omm**. Go to the **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin** directory.

      **cd ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin**

      .. note::

         The version 8.1.2.2 is used as an example. Replace it with the actual version number.

   b. Run the following command to generate and export the server and client certificates of the Flume role:

      **sh geneJKS.sh -f sNetty12@ -g cNetty12@**

      The generated certificate is saved in the **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf** path .

      -  **flume_sChat.jks** is the certificate library of the Flume role server. **flume_sChat.crt** is the exported file of the **flume_sChat.jks** certificate. **-f** indicates the password of the certificate and certificate library.
      -  **flume_cChat.jks** is the certificate library of the Flume role client. **flume_cChat.crt** is the exported file of the **flume_cChat.jks** certificate. **-g** indicates the password of the certificate and certificate library.
      -  **flume_sChatt.jks** and **flume_cChatt.jks** are the SSL certificate trust lists of the Flume server and client, respectively.

      .. note::

         All user-defined passwords involved in this section (such as *sNetty12@*) must meet the following requirements:

         -  The password must contain at least four types of uppercase letters, lowercase letters, digits, and special characters.
         -  The password must contain 8 to 64 characters.
         -  It is recommended that the user-defined passwords be changed periodically (for example, every three months), and certificates and trust lists be generated again to ensure security.

#. Configure the server parameters of the Flume role and upload the configuration file to the cluster.

   a. Remotely log in to any node where the Flume role is located as user **omm** using ECM. Run the following command to go to the ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin directory:

      **cd ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin**

   b. .. _mrs_01_1069__en-us_topic_0000001173631348_l9f81f0e892824e79a1414cd62cce07ba:

      Run the following command to generate and obtain Flume server keystore password, trust list password, and keystore-password encrypted private key information. Enter the password twice and confirm the password. It is the password of the **flume_sChat.jks** certificate library, for example, *sNetty12@*.

      **./genPwFile.sh**

      **cat password.property**

      .. code-block::

         password=D03C2D03D97CBA3F4FD2491A40CAA5E0

   c. Use the Flume configuration tool on the FusionInsight Manager portal to configure the server parameters and generate the configuration file.

      #. Log in to FusionInsight Manager. Choose **Services** > **Flume** > **Configuration Tool**.

      #. Set **Agent Name** to **server**. Select the source, channel, and sink to be used, drag them to the GUI on the right, and connect them.

         For example, use Avro Source, File Channel, and HDFS Sink, as shown in :ref:`Figure 1 <mrs_01_1069__en-us_topic_0000001173631348_f7115f88950ae456f9f3bd83a9a12eb02>`.

         .. _mrs_01_1069__en-us_topic_0000001173631348_f7115f88950ae456f9f3bd83a9a12eb02:

         .. figure:: /_static/images/en-us_image_0000001349059641.png
            :alt: **Figure 1** Example for the Flume configuration tool

            **Figure 1** Example for the Flume configuration tool

      #. Double-click the source, channel, and sink. Set corresponding configuration parameters by seeing :ref:`Table 1 <mrs_01_1069__en-us_topic_0000001173631348_te7d3219190a74a0aba371689e6bdb84d>` based on the actual environment.

         .. note::

            -  If the server parameters of the Flume role have been configured, you can choose **Services** > **Flume** > **Instance** on FusionInsight Manager. Then select the corresponding Flume role instance and click the **Download** button behind the **flume.config.file** parameter on the **Instance Configurations** page to obtain the existing server parameter configuration file. Choose **Services** > **Flume** > **Import** to change the relevant configuration items of encrypted transmission after the file is imported.
            -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.

      #. Click **Export** to save the **properties.properties** configuration file to the local.

         .. _mrs_01_1069__en-us_topic_0000001173631348_te7d3219190a74a0aba371689e6bdb84d:

         .. table:: **Table 1** Parameters to be modified of the Flume role server

            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
            | Parameter             | Description                                                                                                                       | Example Value                                                                                                     |
            +=======================+===================================================================================================================================+===================================================================================================================+
            | ssl                   | Specifies whether to enable the SSL authentication. (You are advised to enable this function to ensure security.)                 | true                                                                                                              |
            |                       |                                                                                                                                   |                                                                                                                   |
            |                       | -  **true** indicates that the function is enabled.                                                                               |                                                                                                                   |
            |                       | -  **false** indicates that the client authentication function is not enabled.                                                    |                                                                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
            | keystore              | Indicates the server certificate.                                                                                                 | ${BIGDATA_HOME\ **}**/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/flume_sChat.jks  |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
            | keystore-password     | Specifies the password of the key library, which is the password required to obtain the keystore information.                     | D03C2D03D97CBA3F4FD2491A40CAA5E0                                                                                  |
            |                       |                                                                                                                                   |                                                                                                                   |
            |                       | Enter the value of password obtained in :ref:`2.b <mrs_01_1069__en-us_topic_0000001173631348_l9f81f0e892824e79a1414cd62cce07ba>`. |                                                                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
            | truststore            | Indicates the SSL certificate trust list of the server.                                                                           | ${BIGDATA_HOME\ **}**/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/flume_sChatt.jks |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
            | truststore-password   | Specifies the trust list password, which is the password required to obtain the truststore information.                           | D03C2D03D97CBA3F4FD2491A40CAA5E0                                                                                  |
            |                       |                                                                                                                                   |                                                                                                                   |
            |                       | Enter the value of password obtained in :ref:`2.b <mrs_01_1069__en-us_topic_0000001173631348_l9f81f0e892824e79a1414cd62cce07ba>`. |                                                                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+

   d. Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Flume**. On the displayed page, click the **Flume** role under **Role**.

   e. Select the Flume role of the node where the configuration file is to be uploaded, choose **Instance Configurations** > **Import** beside the **flume.config.file**, and select the **properties.properties** file.

      .. note::

         -  An independent server configuration file can be uploaded to each Flume instance.
         -  This step is required for updating the configuration file. Modifying the configuration file on the background is an improper operation because the modification will be overwritten after configuration synchronization.

   f. Click **Save**, and then click **OK**. Click **Finish**.

#. Set the client parameters of the Flume role.

   a. Run the following commands to copy the generated client certificate (**flume_cChat.jks**) and client trust list (**flume_cChatt.jks**) to the client directory, for example, **/opt/flume-client/fusionInsight-flume-1.9.0/conf/**. (The Flume client must have been installed.) **10.196.26.1** is the service plane IP address of the node where the client resides.

      **scp ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/flume_cChat.jks user@10.196.26.1:/opt/flume-client/fusionInsight-flume-1.9.0/conf/**

      **scp ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/flume_cChatt.jks user@10.196.26.1:/opt/flume-client/fusionInsight-flume-1.9.0/conf/**

      .. note::

         When copying the client certificate, you need to enter the password of user **user** of the host (for example, **10.196.26.1**) where the client resides.

   b. Log in to the node where the Flume client is decompressed as user **user**. Run the following command to go to the client directory **opt/flume-client/fusionInsight-flume-1.9.0/bin**.

      **cd** **opt/flume-client/fusionInsight-flume-1.9.0/bin**

   c. .. _mrs_01_1069__en-us_topic_0000001173631348_l5265677717ab4dd5971a3b6a0d0be5f6:

      Run the following command to generate and obtain Flume client keystore password, trust list password, and keystore-password encrypted private key information. Enter the password twice and confirm the password. The password is the same as the password of the certificate whose alias is *flumechatclient* and the password of the *flume_cChat.jks* certificate library, for example *cNetty12@*.

      **./genPwFile.sh**

      **cat password.property**

      .. code-block::

         password=4FD2491A40CAA5E0D03C2D03D97CBA3F

      .. note::

         If the following error message is displayed, run the export **JAVA_HOME=\ JDK path** command.

         .. code-block::

            JAVA_HOME is null in current user,please install the JDK and set the JAVA_HOME

   d. Use the Flume configuration tool on FusionInsight Manager to configure the Flume role client parameters and generate a configuration file.

      #. Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Flume** > **Configuration Tool**.

      #. Set **Agent Name** to **client**. Select the source, channel, and sink to be used, drag them to the GUI on the right, and connect them.

         For example, use SpoolDir Source, File Channel, and Avro Sink, as shown in :ref:`Figure 2 <mrs_01_1069__en-us_topic_0000001173631348_f800f39a7cdcf443eab83c9ebcd2211bc>`.

         .. _mrs_01_1069__en-us_topic_0000001173631348_f800f39a7cdcf443eab83c9ebcd2211bc:

         .. figure:: /_static/images/en-us_image_0000001295739988.png
            :alt: **Figure 2** Example for the Flume configuration tool

            **Figure 2** Example for the Flume configuration tool

      #. Double-click the source, channel, and sink. Set corresponding configuration parameters by seeing :ref:`Table 2 <mrs_01_1069__en-us_topic_0000001173631348_t231a870090124a8e8556717e6a7db11c>` based on the actual environment.

         .. note::

            -  If the client parameters of the Flume role have been configured, you can obtain the existing client parameter configuration file from *client installation directory*\ **/fusioninsight-flume-1.9.0/conf/properties.properties** to ensure that the configuration is in concordance with the previous. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Flume** > **Configuration Tool** > **Import**, import the file, and modify the configuration items related to encrypted transmission.
            -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.
            -  A unique checkpoint directory needs to be configured for each File Channel.

      #. Click **Export** to save the **properties.properties** configuration file to the local.

         .. _mrs_01_1069__en-us_topic_0000001173631348_t231a870090124a8e8556717e6a7db11c:

         .. table:: **Table 2** Parameters to be modified of the Flume role client

            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
            | Parameter             | Description                                                                                                                       | Example Value                                                     |
            +=======================+===================================================================================================================================+===================================================================+
            | ssl                   | Indicates whether to enable the SSL authentication. (You are advised to enable this function to ensure security.)                 | true                                                              |
            |                       |                                                                                                                                   |                                                                   |
            |                       | -  **true** indicates that the function is enabled.                                                                               |                                                                   |
            |                       | -  **false** indicates that the client authentication function is not enabled.                                                    |                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
            | keystore              | Specified the client certificate.                                                                                                 | /opt/flume-client/fusionInsight-flume-1.9.0/conf/flume_cChat.jks  |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
            | keystore-password     | Specifies the password of the key library, which is the password required to obtain the keystore information.                     | 4FD2491A40CAA5E0D03C2D03D97CBA3F                                  |
            |                       |                                                                                                                                   |                                                                   |
            |                       | Enter the value of password obtained in :ref:`3.c <mrs_01_1069__en-us_topic_0000001173631348_l5265677717ab4dd5971a3b6a0d0be5f6>`. |                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
            | truststore            | Indicates the SSL certificate trust list of the client.                                                                           | /opt/flume-client/fusionInsight-flume-1.9.0/conf/flume_cChatt.jks |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
            | truststore-password   | Specifies the trust list password, which is the password required to obtain the truststore information.                           | 4FD2491A40CAA5E0D03C2D03D97CBA3F                                  |
            |                       |                                                                                                                                   |                                                                   |
            |                       | Enter the value of password obtained in :ref:`3.c <mrs_01_1069__en-us_topic_0000001173631348_l5265677717ab4dd5971a3b6a0d0be5f6>`. |                                                                   |
            +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+

   e. Upload the **properties.properties** file to **flume/conf/** under the installation directory of the Flume client.

#. Generate the certificate and trust list of the server and client of the MonitorServer role respectively.

   a. Log in to the host using ECM with the MonitorServer role assigned as user **omm**.

      Go to the **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin** directory.

      **cd ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/bin**

   b. Run the following command to generate and export the server and client certificates of the MonitorServer role:

      **sh geneJKS.sh -m sKitty12@ -n cKitty12@**

      The generated certificate is saved in the **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf** path. Where:

      -  **ms_sChat.jks** is the certificate library of the MonitorServer role server. **ms_sChat.crt** is the exported file of the **ms_sChat.jks** certificate. **-m** indicates the password of the certificate and certificate library.
      -  **ms_cChat.jks** is the certificate library of the MonitorServer role client. **ms_cChat.crt** is the exported file of the **ms_cChat.jks** certificate. **-n** indicates the password of the certificate and certificate library.
      -  **ms_sChatt.jks** and **ms_cChatt.jks** are the SSL certificate trust lists of the MonitorServer server and client, respectively.

#. Set the server parameters of the MonitorServer role.

   a. .. _mrs_01_1069__en-us_topic_0000001173631348_l7cc74e0469cb45f4aba9974f2846c1e0:

      Run the following command to generate and obtain MonitorServer server keystore password, trust list password, and keystore-password encrypted private key information. Enter the password twice and confirm the password. The password is the same as the password of the certificate whose alias is *mschatserver* and the password of the *ms_sChat.jks* certificate library, for example *sKitty12@*.

      **./genPwFile.sh**

      **cat password.property**

      .. code-block::

         password=AA5E0D03C2D4FD24CBA3F91A40C03D97

   b. Run the following command to open the ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/service/application.properties file: Modify related parameters based on the description in :ref:`Table 3 <mrs_01_1069__en-us_topic_0000001173631348_tc0d290285ae94086985870f879b563c2>`, save the modification, and exit.

      **vi ${BIGDATA_HOME}/FusionInsight_Porter\_**\ 8.1.2.2\ **/install/FusionInsight-Flume-1.9.0/flume/conf/service/application.properties**

      .. _mrs_01_1069__en-us_topic_0000001173631348_tc0d290285ae94086985870f879b563c2:

      .. table:: **Table 3** Parameters to be modified of the MonitorServer role server

         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | Parameter                           | Description                                                                                                                                                               | Example Value                                                                                            |
         +=====================================+===========================================================================================================================================================================+==========================================================================================================+
         | ssl_need_kspasswd_decrypt_key       | Specifies whether to enable the user-defined key encryption and decryption function. (You are advised to enable this function to ensure security.)                        | true                                                                                                     |
         |                                     |                                                                                                                                                                           |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                       |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                            |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_server_enable                   | Indicates whether to enable the SSL authentication. (You are advised to enable this function to ensure security.)                                                         | true                                                                                                     |
         |                                     |                                                                                                                                                                           |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                       |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                            |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_server_key_store                | Set this parameter based on the specific storage location.                                                                                                                | ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_sChat.jks  |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_server_trust_key_store          | Set this parameter based on the specific storage location.                                                                                                                | ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_sChatt.jks |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_server_key_store_password       | Indicates the client certificate password. Set this parameter based on the actual situation of certificate creation (the plaintext key used to generate the certificate). | AA5E0D03C2D4FD24CBA3F91A40C03D97                                                                         |
         |                                     |                                                                                                                                                                           |                                                                                                          |
         |                                     | Enter the value of password obtained in :ref:`5.a <mrs_01_1069__en-us_topic_0000001173631348_l7cc74e0469cb45f4aba9974f2846c1e0>`.                                         |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_server_trust_key_store_password | Specifies the trustkeystore password. Set this parameter based on the actual situation of certificate creation (the plaintext key used to generate the trust list).       | AA5E0D03C2D4FD24CBA3F91A40C03D97                                                                         |
         |                                     |                                                                                                                                                                           |                                                                                                          |
         |                                     | Enter the value of password obtained in :ref:`5.a <mrs_01_1069__en-us_topic_0000001173631348_l7cc74e0469cb45f4aba9974f2846c1e0>`.                                         |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_need_client_auth                | Indicates whether to enable the client authentication. (You are advised to enable this function to ensure security.)                                                      | true                                                                                                     |
         |                                     |                                                                                                                                                                           |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                       |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                            |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+

   c. Restart the MonitorServer instance. Choose **Services** > **Flume** > **Instance** > **MonitorServer**, select the MonitorServer instance, and choose **More** > **Restart Instance**. Enter the system administrator password and click **OK**. After the restart is complete, click **Finish**.

#. Set the client parameters of the MonitorServer role.

   a. Run the following commands to copy the generated client certificate (**ms_cChat.jks**) and client trust list (**ms_cChatt.jks**) to the **/opt/flume-client/fusionInsight-flume-1.9.0/conf/** client directory. **10.196.26.1** is the service plane IP address of the node where the client resides.

      **scp ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_cChat.jks user@10.196.26.1:/opt/flume-client/fusionInsight-flume-1.9.0/conf/**

      **scp ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_cChatt.jks user@10.196.26.1:/opt/flume-client/fusionInsight-flume-1.9.0/conf/**

   b. Log in to the node where the Flume client is located as **user**. Run the following command to go to the client directory **/opt/flume-client/fusionInsight-flume-1.9.0/bin**.

      **cd** **/opt/flume-client/fusionInsight-flume-1.9.0/bin**

   c. .. _mrs_01_1069__en-us_topic_0000001173631348_l252c5a768cc34fcca9cfaa5a90dfe8c0:

      Run the following command to generate and obtain MonitorServer client keystore password, trust list password, and keystore-password encrypted private key information. Enter the password twice and confirm the password. The password is the same as the password of the certificate whose alias is *mschatclient* and the password of the *ms_cChat.jks* certificate library, for example *cKitty12@*.

      **./genPwFile.sh**

      **cat password.property**

      .. code-block::

         password=BA3F91A40C03D97AA5E0D03C2D4FD24C

   d. Run the following command to open the **/opt/flume-client/fusionInsight-flume-1.9.0/conf/service/application.properties** file. (**/opt/flume-client/fusionInsight-flume-1.9.0** is the directory where the client software is installed.) Modify related parameters based on the description in :ref:`Table 4 <mrs_01_1069__en-us_topic_0000001173631348_tea1b721973a843b7891ab85f51d2f2e6>`, save the modification, and exit.

      **vi** **/opt/flume-client/fusionInsight-flume-1.9.0/flume/conf/service/application.properties**

      .. _mrs_01_1069__en-us_topic_0000001173631348_tea1b721973a843b7891ab85f51d2f2e6:

      .. table:: **Table 4** Parameters to be modified of the MonitorServer role client

         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | Parameter                           | Description                                                                                                                                                         | Example Value                                                                                            |
         +=====================================+=====================================================================================================================================================================+==========================================================================================================+
         | ssl_need_kspasswd_decrypt_key       | Indicates whether to enable the user-defined key encryption and decryption function. (You are advised to enable this function to ensure security.)                  | true                                                                                                     |
         |                                     |                                                                                                                                                                     |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                 |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                      |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_client_enable                   | Indicates whether to enable the SSL authentication. (You are advised to enable this function to ensure security.)                                                   | true                                                                                                     |
         |                                     |                                                                                                                                                                     |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                 |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                      |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_client_key_store                | Set this parameter based on the specific storage location.                                                                                                          | ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_cChat.jks  |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_client_trust_key_store          | Set this parameter based on the specific storage location.                                                                                                          | ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Flume-1.9.0/flume/conf/ms_cChatt.jks |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_client_key_store_password       | Specifies the keystore password. Set this parameter based on the actual situation of certificate creation (the plaintext key used to generate the certificate).     | BA3F91A40C03D97AA5E0D03C2D4FD24C                                                                         |
         |                                     |                                                                                                                                                                     |                                                                                                          |
         |                                     | Enter the value of **password** obtained in :ref:`6.c <mrs_01_1069__en-us_topic_0000001173631348_l252c5a768cc34fcca9cfaa5a90dfe8c0>`.                               |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_client_trust_key_store_password | Specifies the trustkeystore password. Set this parameter based on the actual situation of certificate creation (the plaintext key used to generate the trust list). | BA3F91A40C03D97AA5E0D03C2D4FD24C                                                                         |
         |                                     |                                                                                                                                                                     |                                                                                                          |
         |                                     | Enter the value of **password** obtained in :ref:`6.c <mrs_01_1069__en-us_topic_0000001173631348_l252c5a768cc34fcca9cfaa5a90dfe8c0>`.                               |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
         | ssl_need_client_auth                | Indicates whether to enable the client authentication. (You are advised to enable this function to ensure security.)                                                | true                                                                                                     |
         |                                     |                                                                                                                                                                     |                                                                                                          |
         |                                     | -  **true** indicates that the function is enabled.                                                                                                                 |                                                                                                          |
         |                                     | -  **false** indicates that the client authentication function is not enabled.                                                                                      |                                                                                                          |
         +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+
