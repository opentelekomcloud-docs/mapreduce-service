:original_name: admin_guide_000014.html

.. _admin_guide_000014:

Downloading the Client
======================

Scenario
--------

Use the default client provided by MRS clusters to manage the cluster, run services, and perform secondary development. Before you use this client, you need to download its software package.

Procedure
---------

#. Log in to MRS Manager.

#. In the upper right corner of the home page, click \ **Download Client**\ .

   The **Download Cluster Client** dialog box is displayed.

#. Select a client type for **Select Client Type**.

   -  **Complete Client**: the package contains scripts, compilation files, and configuration files.

   -  **Configuration Files Only**: the package contains only the client configuration files.

      This type is applicable to application development tasks. For example, after a complete client is downloaded and installed, the cluster administrator modifies the service configuration on MRS Manager, and developers need to update the client configuration files.

   .. note::

      Set **Select Platform Type** to **x86_64** or **aarch64**. To run the client on x86 nodes, select **x86_64**; to tun the client on TaiShan nodes, select **aarch64**. By default, you should select a client that has the same architecture as your servers.

#. Select the path for downloading the client file and set related parameters. Click \ **OK**\ . For MRS 3.5.0 and later versions, perform this step. For versions earlier than MRS 3.5.0, go to :ref:`5 <admin_guide_000014__ld012ac11d5964bfb8aa92456bfc341fb>`.

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

#. .. _admin_guide_000014__ld012ac11d5964bfb8aa92456bfc341fb:

   Determine whether to generate a client software package file on the cluster node. For versions earlier than MRS 3.5.0, perform this step.

   -  If yes, select **Save to Path** and click **OK** to generate the client file.

      The generated file is stored in the **/tmp/FusionInsight-Client** directory on the active management node by default. You can also store the client file in other directories, and user **omm** has the read, write, and execute permissions on the directory. If the client file already exists in the path, the existing client file will be replaced.

      After the file is generated, copy the obtained package to another directory, for example, **/opt/Bigdata/hadoopclient**, as user **omm** or client installation user.

   -  If no, click **OK** to download the client file to the local host.

      The system starts to download the client software package.

   Install the downloaded client by referring to :ref:`Installing a Client <admin_guide_000171>`.
