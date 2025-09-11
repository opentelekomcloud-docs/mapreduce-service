:original_name: admin_guide_000173.html

.. _admin_guide_000173:

Updating the Configuration of an Installed Client
=================================================

Scenario
--------

The cluster provides a client for you to connect to a server, view task results, or manage data. If you modify service configuration parameters on MRS Manager and restart the service, you need to download and install the installed client again or use the configuration file to update the client.

Prerequisites
-------------

You have installed a client.

Procedure
---------

**Method 1**:

#. Log in to MRS Manager. Click the wanted cluster from the **Cluster** drop-down list.

#. Click **More** and select **Download Client**. In the **Download Cluster Client** dialog box, select **Configuration Files Only**.

   The generated compressed file contains the configuration files of all services.

#. Select the path for saving the downloaded client configuration file.

   -  **Server**: Download the file to the active OMS node of the cluster.

      The generated file is stored in the **/tmp/FusionInsight-Client** directory on the active OMS node by default. You can also store the client file in other directories, and user **omm** has the read, write, and execute permissions on the directory. If the client file already exists in the path, the existing client file will be replaced.

      .. note::

         When a cluster has many services installed, the cluster client file becomes quite large. Additionally, decompressing this file during installation can consume significant disk space. It's recommended to download the client files to a different directory that has ample space, or to promptly remove unnecessary files from the client download directory after installation. Doing so helps avoid exhausting the **/tmp directory**'s disk space, which could interrupt the normal operation of the cluster nodes.

      After the file is generated, copy the obtained package to another directory, for example, **/opt/Bigdata/hadoopclient**, as user **omm** or client installation user.

   -  **Browser**: Download the file to the local computer.

   -  **Remote node:** Download the file to a node other than the active OMS node. If you select this option, you need to set the following parameters:

      .. table:: **Table 1** Parameters

         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Parameter             | Description                                                                                                                                                                   | Example Value                     |
         +=======================+===============================================================================================================================================================================+===================================+
         | Save to Path          | Path for storing client files.                                                                                                                                                | /tmp/FusionInsight-Client-Remote/ |
         |                       |                                                                                                                                                                               |                                   |
         |                       | If there is already a client file in the path, it will be overwritten. For a remote node, write permission for the path is required.                                          |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Host IP Address       | IP address of the remote node.                                                                                                                                                | x.x.x.x                           |
         |                       |                                                                                                                                                                               |                                   |
         |                       | .. note::                                                                                                                                                                     |                                   |
         |                       |                                                                                                                                                                               |                                   |
         |                       |    The platform type of the remote node must be the same as that of the downloaded client. Otherwise, the client may fail to be installed.                                    |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Host Port             | Host port of the remote node.                                                                                                                                                 | 22                                |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Username              | Username for logging in to the remote node.                                                                                                                                   | xxx                               |
         |                       |                                                                                                                                                                               |                                   |
         |                       | For a remote node, write permission for the path is required.                                                                                                                 |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Authentication Method | You can choose one of the following methods:                                                                                                                                  | Password                          |
         |                       |                                                                                                                                                                               |                                   |
         |                       | -  **Password**: Use the password for login.                                                                                                                                  |                                   |
         |                       | -  **SSH private keys**: Use SSH private keys for login.                                                                                                                      |                                   |
         |                       | -  **None**: To use this method, passwordless login needs to be enabled for the node.                                                                                         |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Password              | This parameter is mandatory when **Authentication Method** is set to **Password**.                                                                                            | xxx                               |
         |                       |                                                                                                                                                                               |                                   |
         |                       | This parameter indicates the password used for login.                                                                                                                         |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | SSH Private Keys      | This parameter is mandatory when **Authentication Method** is set to **SSH private keys**.                                                                                    | ``-``                             |
         |                       |                                                                                                                                                                               |                                   |
         |                       | Click **Select File** and select a local file to upload.                                                                                                                      |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Auto Deployment       | Whether to enable auto deployment. This parameter is mandatory when **Select Client Type** is set to **Complete Client**.                                                     | Yes                               |
         |                       |                                                                                                                                                                               |                                   |
         |                       | -  If you set this parameter to **yes**, the client is automatically installed and deployed on the current node.                                                              |                                   |
         |                       | -  If you set this parameter to **no**, the client will not be automatically installed and deployed. You need to manually install the client after it is downloaded.          |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Deployment Path       | This parameter is mandatory when **Auto Deployment** is set to **Yes**. If only the configuration file is downloaded, this parameter will not be displayed.                   | /opt/testclient                   |
         |                       |                                                                                                                                                                               |                                   |
         |                       | The deployment path must be empty if it already exists on the remote node. Otherwise, it will be created automatically. The path also requires operate and write permissions. |                                   |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+

#. Use WinSCP to save the compressed file to the installation directory of the client as the client installation user, such as **/opt/hadoopclient**.

#. Decompress the software package.

   Run the following commands to go to the directory where the client is installed, and decompress the file to a local directory. For example, the downloaded client file is **FusionInsight_Cluster_1_Services_Client.tar**.

   **cd /opt/hadoopclient**

   **tar -xvf** **FusionInsight_Cluster_1\_Services_Client.tar**

#. Verify the software package.

   Run the following command to verify the decompressed file and check whether the command output is consistent with the information in the **sha256** file:

   **sha256sum -c** **FusionInsight\_\ Cluster_1\_\ Services_ClientConfig_ConfigFiles.tar.sha256**

   .. code-block::

      FusionInsight_Cluster_1_Services_ClientConfig_ConfigFiles.tar: OK

#. Decompress the package to obtain the configuration file.

   **tar -xvf FusionInsight\_\ Cluster_1\_\ Services_ClientConfig_ConfigFiles.tar**

#. Run the following command in the client installation directory to update the client using the configuration file:

   **sh refreshConfig.sh** *Client installation directory* *Directory where the configuration file is located*

   For example, run the following command:

   **sh refreshConfig.sh** **/opt/hadoopclient /opt/hadoop\ client/FusionInsight\_Cluster_1_Services_ClientConfig\_ConfigFiles**

   If the following information is displayed, the configurations have been updated successfully:

   .. code-block::

      Succeed to refresh components client config.

**Method 2**:

#. Log in to the node where the client is installed as user **root**.

#. Go to the client installation directory, for example, **/opt/client**, and run the following commands to update the configuration file:

   **cd /opt/client**

   **sh autoRefreshConfig.sh**

#. Enter the username and password of the MRS Manager administrator and the floating IP address of MRS Manager.

#. Enter the names of the components whose configurations need to be updated. Use commas (,) to separate the component names. Press **Enter** to update the configurations of all components if necessary.

   If the following information is displayed, the configurations have been updated successfully:

   .. code-block::

      Succeed to refresh components client config.
