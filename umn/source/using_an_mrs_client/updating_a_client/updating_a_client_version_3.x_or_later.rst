:original_name: mrs_01_24209.html

.. _mrs_01_24209:

Updating a Client (Version 3.x or Later)
========================================

A cluster provides a client for you to connect to a server, view task results, or manage data. If you modify service configuration parameters on Manager and restart the service, you need to download and install the client again or use the configuration file to update the client.

Updating the Client Configuration
---------------------------------

**Method 1**:

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_0129>`. Click the name of the cluster to be operated in the **Cluster** drop-down list.

#. Choose **More** > **Download Client** > **Configuration Files Only**.

   The generated compressed file contains the configuration files of all services.

#. Determine whether to generate a configuration file on the cluster node.

   -  If yes, select **Save to Path**, and click **OK** to generate the client file. By default, the client file is generated in **/tmp/FusionInsight-Client** on the active management node. You can also store the client file in other directories, and user **omm** has the read, write, and execute permissions on the directories. Then go to :ref:`4 <mrs_01_24209__admin_guide_000173_en-us_topic_0193213946_l6af983f03121493ca3526296f5b650c3>`.
   -  If no, click **OK**, specify a local save path, and download the complete client. Wait until the download is complete and go to :ref:`4 <mrs_01_24209__admin_guide_000173_en-us_topic_0193213946_l6af983f03121493ca3526296f5b650c3>`.

#. .. _mrs_01_24209__admin_guide_000173_en-us_topic_0193213946_l6af983f03121493ca3526296f5b650c3:

   Use WinSCP to save the compressed file to the client installation directory, for example, **/opt/hadoopclient**, as the client installation user.

#. Decompress the software package.

   Run the following commands to go to the directory where the client is installed, and decompress the file to a local directory. For example, the downloaded client file is **FusionInsight_Cluster_1_Services_Client.tar**.

   **cd /opt/hadoopclient**

   **tar -xvf** **FusionInsight_Cluster_1\_Services_Client.tar**

#. Verify the software package.

   Run the following command to verify the decompressed file and check whether the command output is consistent with the information in the **sha256** file.

   **sha256sum -c** **FusionInsight\_\ Cluster_1\_\ Services_ClientConfig_ConfigFiles.tar.sha256**

   .. code-block::

      FusionInsight_Cluster_1_Services_ClientConfig_ConfigFiles.tar: OK

#. Decompress the package to obtain the configuration file.

   **tar -xvf FusionInsight\_\ Cluster_1\_\ Services_ClientConfig_ConfigFiles.tar**

#. Run the following command in the client installation directory to update the client using the configuration file:

   **sh refreshConfig.sh** *Client installation directory* *Directory where the configuration file is located*

   For example, run the following command:

   **sh refreshConfig.sh** **/opt/hadoopclient /opt/hadoop\ client/FusionInsight\_Cluster_1_Services_ClientConfig\_ConfigFiles**

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      Succeed to refresh components client config.

**Method 2**:

#. Log in to the client installation node as user **root**.

#. Go to the client installation directory, for example, **/opt/hadoopclient** and run the following commands to update the configuration file:

   **cd /opt/hadoopclient**

   **sh autoRefreshConfig.sh**

#. Enter the username and password of the FusionInsight Manager administrator and the floating IP address of FusionInsight Manager.

#. Enter the names of the components whose configuration needs to be updated. Use commas (,) to separate the component names. Press **Enter** to update the configurations of all components if necessary.

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      Succeed to refresh components client config.
