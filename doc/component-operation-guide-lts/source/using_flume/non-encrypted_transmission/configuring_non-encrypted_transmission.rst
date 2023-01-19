:original_name: mrs_01_1060.html

.. _mrs_01_1060:

Configuring Non-encrypted Transmission
======================================

Scenario
--------

This section describes how to configure Flume server and client parameters after the cluster and the Flume service are installed to ensure proper running of the service.

.. note::

   By default, the cluster network environment is secure and the SSL authentication is not enabled during the data transmission process. For details about how to use the encryption mode, see :ref:`Configuring the Encrypted Transmission <mrs_01_1069>`.

Prerequisites
-------------

-  The cluster and Flume service have been installed.
-  The network environment of the cluster is secure.

Procedure
---------

#. Configure the client parameters of the Flume role.

   a. Use the Flume configuration tool on FusionInsight Manager to configure the Flume role client parameters and generate a configuration file.

      #. Log in to FusionInsight Manager. Choose **Cluster** > **Services** > **Flume** > **Configuration Tool**.

      #. Set **Agent Name** to **client**. Select and drag the source, channel, and sink to be used to the GUI on the right, and connect them.

         For example, use SpoolDir Source, File Channel, and Avro Sink, as shown in :ref:`Figure 1 <mrs_01_1060__en-us_topic_0000001173949126_f48a8b06747cd425f9ce3e09139d567fe>`.

         .. _mrs_01_1060__en-us_topic_0000001173949126_f48a8b06747cd425f9ce3e09139d567fe:

         .. figure:: /_static/images/en-us_image_0000001296059860.png
            :alt: **Figure 1** Example for the Flume configuration tool

            **Figure 1** Example for the Flume configuration tool

      #. Double-click the source, channel, and sink. Set corresponding configuration parameters by referring to :ref:`Table 1 <mrs_01_1060__en-us_topic_0000001173949126_td6a1d78a7c28412b91ec3b4ecdfdfef1>` based on the actual environment.

         .. note::

            -  If the client parameters of the Flume role have been configured, you can obtain the existing client parameter configuration file from *client installation directory*\ **/fusioninsight-flume-1.9.0/conf/properties.properties** to ensure that the configuration is in concordance with the previous. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Flume** > **Configuration** > **Import**, import the file, and modify the configuration items related to non-encrypted transmission.
            -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.

      #. Click **Export** to save the **properties.properties** configuration file to the local server.

         .. _mrs_01_1060__en-us_topic_0000001173949126_td6a1d78a7c28412b91ec3b4ecdfdfef1:

         .. table:: **Table 1** Parameters to be modified of the Flume role client

            +-----------------------+-------------------------------------------------------------------------------------------------------------------+-----------------------+
            | Parameter             | Description                                                                                                       | Example Value         |
            +=======================+===================================================================================================================+=======================+
            | ssl                   | Specifies whether to enable the SSL authentication. (You are advised to enable this function to ensure security.) | false                 |
            |                       |                                                                                                                   |                       |
            |                       | Only Sources of the Avro type have this configuration item.                                                       |                       |
            |                       |                                                                                                                   |                       |
            |                       | -  **true** indicates that the function is enabled.                                                               |                       |
            |                       | -  **false** indicates that the function is not enabled.                                                          |                       |
            +-----------------------+-------------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Upload the **properties.properties** file to **flume/conf/** under the installation directory of the Flume client.

#. Configure the server parameters of the Flume role and upload the configuration file to the cluster.

   a. Use the Flume configuration tool on the FusionInsight Manager portal to configure the server parameters and generate the configuration file.

      #. Log in to FusionInsight Manager. Choose **Cluster** > **Services** > **Flume** > **Configuration Tool**.

      #. Set **Agent Name** to **server**. Select and drag the source, channel, and sink to be used to the GUI on the right, and connect them.

         For example, use Avro Source, File Channel, and HDFS Sink, as shown in :ref:`Figure 2 <mrs_01_1060__en-us_topic_0000001173949126_fc16f89e37d8b45e4ab9853d9d2a4824d>`.

         .. _mrs_01_1060__en-us_topic_0000001173949126_fc16f89e37d8b45e4ab9853d9d2a4824d:

         .. figure:: /_static/images/en-us_image_0000001349259161.png
            :alt: **Figure 2** Example for the Flume configuration tool

            **Figure 2** Example for the Flume configuration tool

      #. Double-click the source, channel, and sink. Set corresponding configuration parameters by referring to :ref:`Table 2 <mrs_01_1060__en-us_topic_0000001173949126_tc4c29f50094a4d978a0048c9f8652714>` based on the actual environment.

         .. note::

            -  If the server parameters of the Flume role have been configured, you can choose **Cluster** > **Services** > **Flume** > **Instance** on FusionInsight Manager. Then select the corresponding Flume role instance and click the **Download** button behind the **flume.config.file** parameter on the **Instance Configurations** page to obtain the existing server parameter configuration file. Choose **Cluster** > **Service** > **Flume** > **Configurations** > **Import**, import the file, and modify the configuration items related to non-encrypted transmission.
            -  It is recommended that the numbers of Sources, Channels, and Sinks do not exceed 40 during configuration file import. Otherwise, the response time may be very long.
            -  A unique checkpoint directory needs to be configured for each File Channel.

      #. Click **Export** to save the **properties.properties** configuration file to the local server.

         .. _mrs_01_1060__en-us_topic_0000001173949126_tc4c29f50094a4d978a0048c9f8652714:

         .. table:: **Table 2** Parameters to be modified of the Flume role server

            +-----------------------+-------------------------------------------------------------------------------------------------------------------+-----------------------+
            | Parameter             | Description                                                                                                       | Example Value         |
            +=======================+===================================================================================================================+=======================+
            | ssl                   | Specifies whether to enable the SSL authentication. (You are advised to enable this function to ensure security.) | false                 |
            |                       |                                                                                                                   |                       |
            |                       | Only Sources of the Avro type have this configuration item.                                                       |                       |
            |                       |                                                                                                                   |                       |
            |                       | -  **true** indicates that the function is enabled.                                                               |                       |
            |                       | -  **false** indicates that the function is not enabled.                                                          |                       |
            +-----------------------+-------------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Flume**. On the **Instances** tab page, click **Flume**.
   c. Select the Flume role of the node where the configuration file is to be uploaded, choose **Instance Configurations** > **Import** beside the **flume.config.file**, and select the **properties.properties** file.

      .. note::

         -  An independent server configuration file can be uploaded to each Flume instance.
         -  This step is required for updating the configuration file. Modifying the configuration file on the background is an improper operation because the modification will be overwritten after configuration synchronization.

   d. Click **Save**, and then click **OK**.
   e. Click **Finish**.
