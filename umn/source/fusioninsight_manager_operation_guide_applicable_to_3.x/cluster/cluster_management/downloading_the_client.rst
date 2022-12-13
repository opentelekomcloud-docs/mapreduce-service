:original_name: admin_guide_000014.html

.. _admin_guide_000014:

Downloading the Client
======================

Scenario
--------

Use the default client provided by MRS clusters to manage the cluster, run services, and perform secondary development. Before you use this client, you need to download its software package.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Dashboard**. On the page that is displayed, choose **More** > **Download Client**.

   The **Download Cluster Client** dialog box is displayed.

#. Select a client type for **Select Client Type**.

   -  **Complete Client**: the package contains scripts, compilation files, and configuration files.

   -  **Configuration Files Only**: the package contains only the client configuration files.

      This type is applicable to application development tasks. For example, after a complete client is downloaded and installed, the cluster administrator modifies the service configuration on FusionInsight Manager, and developers need to update the client configuration files.

   .. note::

      Set **Select Platform Type** to **x86_64** or **aarch64**. To run the client on x86 nodes, select **x86_64**; to tun the client on TaiShan nodes, select **aarch64**. By default, you should select a client that has the same architecture as your servers.

#. Determine whether to generate a client software package file on the cluster node.

   -  If yes, select **Save to Path** and click **OK** to generate the client file.

      The generated file is stored in the **/tmp/FusionInsight-Client** directory on the active management node by default. You can also store the client file in other directories, and user **omm** has the read, write, and execute permissions on the directory. If the client file already exists in the path, the existing client file will be replaced.

      After the file is generated, copy the obtained package to another directory, for example, **/opt/Bigdata/hadoopclient**, as user **omm** or client installation user.

   -  If no, click **OK** to download the client file to the local host.

      The system starts to download the client software package.

   Install the downloaded client by referring to :ref:`Installing a Client <admin_guide_000171>`.
