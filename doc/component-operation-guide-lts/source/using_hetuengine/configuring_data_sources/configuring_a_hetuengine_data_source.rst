:original_name: mrs_01_1719.html

.. _mrs_01_1719:

Configuring a HetuEngine Data Source
====================================

Scenario
--------

This section describes how to add another HetuEngine data source on the HSConsole page for a cluster in security mode.

Currently, the following data sources are supported: boolean, tinyint, smallint, int, bigint, real, double, decimal, varchar, char, date, timestamp, array, map, time with timezone, timestamp with time zone, and Time.

Procedure
---------

#. .. _mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_li3754145741715:

   Obtain the **user.keytab** file of the proxy user of the HetuEngine cluster in a remote domain.

   a. Log in to FusionInsight Manager of the HetuEngine cluster in the remote domain.
   b. Choose **System** > **Permission** > **User**.
   c. Locate the row that contains the target data source user, click **More** in the **Operation** column, and select **Download Authentication Credential**.
   d. The **user.keytab** file extracted from the downloaded file is the user credential file.

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.

#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

#. Choose **Data Source** and click **Add Data Source**. Configure parameters on the **Add Data Source** page.

   a. Configure **Basic Information**. For details, see :ref:`Table 1 <mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_en-us_topic_0260386270_table14393741174611>`.

      .. _mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_en-us_topic_0260386270_table14393741174611:

      .. table:: **Table 1** Basic Information

         +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter             | Description                                                                                                                                                                                                                                        | Example Value         |
         +=======================+====================================================================================================================================================================================================================================================+=======================+
         | Name                  | Name of the data source to be connected.                                                                                                                                                                                                           | hetu_1                |
         |                       |                                                                                                                                                                                                                                                    |                       |
         |                       | The value can contain only letters, digits, and underscores (_) and must start with a letter. If the data source name contains uppercase letters, the background automatically converts the uppercase letters to lowercase letters during storage. |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Data Source Type      | Type of the data source to be connected. Select **HetuEngine**.                                                                                                                                                                                    | HetuEngine            |
         +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Mode                  | Mode of the current cluster. The security mode is used by default.                                                                                                                                                                                 | Security Mode         |
         +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Description           | Description of the data source.                                                                                                                                                                                                                    | ``-``                 |
         |                       |                                                                                                                                                                                                                                                    |                       |
         |                       | The value can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks.                                                                                                                                     |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Configure parameters in the **HetuEngine Configuration** area. For details, see :ref:`Table 2 <mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_en-us_topic_0260386270_table0303122318010>`.

      .. _mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_en-us_topic_0260386270_table0303122318010:

      .. table:: **Table 2** HetuEngine Configuration

         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter                  | Description                                                                                                                                                                                                                               | Example Value         |
         +============================+===========================================================================================================================================================================================================================================+=======================+
         | Driver                     | The default value is **hsfabric-initial**.                                                                                                                                                                                                | hsfabric-initial      |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Username                   | Configure this parameter when the security mode is enabled.                                                                                                                                                                               | hetu_test             |
         |                            |                                                                                                                                                                                                                                           |                       |
         |                            | It specifies the user who accesses the remote HetuEngine. Set the parameter to the user to whom the **user.keytab** file obtained in :ref:`1 <mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_li3754145741715>` belongs. |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Keytab File                | Configure this parameter when the security mode is enabled.                                                                                                                                                                               | user.keytab           |
         |                            |                                                                                                                                                                                                                                           |                       |
         |                            | This is the Keytab file of the user who accesses the remote DataCenter. Select the **user.keytab** file obtained in :ref:`1 <mrs_01_1719__en-us_topic_0000001173631388_en-us_topic_0260680339_li3754145741715>`.                          |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Two Way Transmission       | This parameter indicates whether to enable bidirectional transmission for cross-domain data transmission. The default value is **Yes**.                                                                                                   | Yes                   |
         |                            |                                                                                                                                                                                                                                           |                       |
         |                            | -  **Yes**: Two-way transmission: Requests are forwarded to the remote HSFabric through the local HSFabric. If two-way transmission is enabled, the local HSFabric address must be configured.                                            |                       |
         |                            | -  No: Unidirectional transmission: Requests are directly sent to the remote HSFabric.                                                                                                                                                    |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Local Configuration        | Host IP address and port number of the HSFabric instance that is responsible for external communication of the HetuEngine service in the local MRS cluster.                                                                               | 192.162.157.32:29900  |
         |                            |                                                                                                                                                                                                                                           |                       |
         |                            | #. Log in to FusionInsight Manager of the local cluster, choose **Cluster** > **Services** > **HetuEngine** > **Instance**, and check the service IP address of the HSFabric.                                                             |                       |
         |                            | #. Click **HSFabric**, choose **Instance Configuration**, and check the value of **server.port**. The default value is **29900**.                                                                                                         |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Remote Address             | Host IP address and port number of the HSFabric instance that is responsible for external communication of the HetuEngine service in the remote MRS cluster.                                                                              | 192.168.1.1:29900     |
         |                            |                                                                                                                                                                                                                                           |                       |
         |                            | #. Log in to FusionInsight Manager of the remote cluster, choose **Cluster** > **Services** > **HetuEngine** > **Instance**, and check the service IP address of the HSFabric.                                                            |                       |
         |                            | #. Click **HSFabric**, choose **Instance Configuration**, and check the value of **server.port**. The default value is **29900**.                                                                                                         |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Region                     | Region to which the current request initiator belongs. The value can contain only digits and underscores (_).                                                                                                                             | 0755_01               |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Receiving Data Timeout (s) | Timeout interval for receiving data, in seconds.                                                                                                                                                                                          | 60                    |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Total Task Timeout (s)     | Total timeout duration for executing a cross-domain task, in seconds.                                                                                                                                                                     | 300                   |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Tasks Used by Worker Nodes | Number of tasks used by each worker node to receive data.                                                                                                                                                                                 | 5                     |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Data Compression           | -  **Yes**: Data compression is enabled.                                                                                                                                                                                                  | Yes                   |
         |                            | -  **No**: Data compression is disabled.                                                                                                                                                                                                  |                       |
         +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   c. Modify custom configurations.

      -  You can click **Add** to add custom configuration parameters. Configure custom parameters of the HetuEngine data source. For details, see :ref:`Table 3 <mrs_01_1719__en-us_topic_0000001173631388_table107221036132419>`.

         .. _mrs_01_1719__en-us_topic_0000001173631388_table107221036132419:

         .. table:: **Table 3** Custom parameters of the HetuEngine data source

            +----------------------------+------------------------------------------------------------------------------------+-----------------------+
            | Parameter                  | Description                                                                        | Example Value         |
            +============================+====================================================================================+=======================+
            | hsfabric.health.check.time | Interval for checking the HSFabric instance status, in seconds.                    | 60                    |
            +----------------------------+------------------------------------------------------------------------------------+-----------------------+
            | hsfabric.subquery.pushdown | Whether to enable cross-domain query pushdown. The function is enabled by default. | true                  |
            |                            |                                                                                    |                       |
            |                            | -  **true**: enables cross-domain query pushdown.                                  |                       |
            |                            | -  **false**: disables cross-domain query pushdown.                                |                       |
            +----------------------------+------------------------------------------------------------------------------------+-----------------------+

      -  You can click **Delete** to delete custom configuration parameters.

   d. Click **OK**.
