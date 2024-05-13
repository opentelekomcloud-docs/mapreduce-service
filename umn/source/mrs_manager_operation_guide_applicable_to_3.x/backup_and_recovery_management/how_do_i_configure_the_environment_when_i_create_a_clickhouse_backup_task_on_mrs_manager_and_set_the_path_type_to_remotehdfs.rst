:original_name: admin_guide_000357.html

.. _admin_guide_000357:

How Do I Configure the Environment When I Create a ClickHouse Backup Task on MRS Manager and Set the Path Type to RemoteHDFS?
=============================================================================================================================

.. note::

   This section applies only to MRS 3.1.0.

Question
--------

How do I configure the environment when I create a ClickHouse backup task on MRS Manager and set the path type to RemoteHDFS?

Answer
------

#. Log in to MRS Manager of the standby cluster.

#. Choose **Cluster** > **Services** > **HDFS** and choose **More** > **Download Client**. Set **Select Client Type** to **Configuration Files Only**, select **x86_64** for x86 or **aarch64** for ARM based on the type of the node where the client is to be installed, and click **OK**.

#. After the client file package is generated, download the client to the local PC as prompted and decompress the package.

   For example, if the client file package is **FusionInsight_Cluster_1_HDFS_Client.tar**, decompress it to obtain **FusionInsight_Cluster_1_HDFS_ClientConfig_ConfigFiles.tar**, and then decompress **FusionInsight_Cluster_1_HDFS_ClientConfig_ConfigFiles.tar** to the **D:\\FusionInsight_Cluster_1_HDFS_ClientConfig_ConfigFiles** directory on the local PC. The directory name cannot contain spaces.

#. .. _admin_guide_000357__li73411714152720:

   Go to the **FusionInsight_Cluster_1_HDFS_ClientConfig_ConfigFiles\\** client directory and obtain the **hosts** file.

#. Log in to MRS Manager of the source cluster.

#. Choose **Cluster** > **Services** > **ClickHouse**, click **Instance**, and view the instance IP address of **ClickHouseServer**.

#. Log in to the host nodes of the ClickHouseServer instances as user **root** and check whether the **/etc/hosts** file contains the host information in :ref:`4 <admin_guide_000357__li73411714152720>`. If not, add the host information in :ref:`4 <admin_guide_000357__li73411714152720>` to the **/etc/hosts** file.
