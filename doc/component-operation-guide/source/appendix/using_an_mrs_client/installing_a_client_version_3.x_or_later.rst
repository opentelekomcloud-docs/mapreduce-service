:original_name: mrs_01_2127.html

.. _mrs_01_2127:

Installing a Client (Version 3.x or Later)
==========================================

Scenario
--------

This section describes how to install clients of all services (excluding Flume) in an MRS cluster. For details about how to install the Flume client, see `Installing the Flume Client <https://docs.otc.t-systems.com/cmpntguide/mrs/mrs_01_0392.html>`__.

A client can be installed on a node inside or outside the cluster. This section uses the installation directory **//opt/client** as an example. Replace it with the actual one.

.. _mrs_01_2127__en-us_topic_0264269828_en-us_topic_0270713152_en-us_topic_0264269418_section3219221104310:

Prerequisites
-------------

-  A Linux ECS has been prepared. For details about the supported OS of the ECS, see :ref:`Table 1 <mrs_01_2127__en-us_topic_0264269828_en-us_topic_0270713152_en-us_topic_0264269418_table40818788104630>`.

   .. _mrs_01_2127__en-us_topic_0264269828_en-us_topic_0270713152_en-us_topic_0264269418_table40818788104630:

   .. table:: **Table 1** Reference list

      ================ ====== ===============================================
      CPU Architecture OS     Supported Version
      ================ ====== ===============================================
      x86 computing    Euler  EulerOS 2.5
      \                SUSE   SUSE Linux Enterprise Server 12 SP4 (SUSE 12.4)
      \                RedHat Red Hat-7.5-x86_64 (Red Hat 7.5)
      \                CentOS CentOS 7.6
      ================ ====== ===============================================

   In addition, sufficient disk space is allocated for the ECS, for example, 40 GB.

-  The ECS and the MRS cluster are in the same VPC.

-  The security group of the ECS must be the same as that of the master node in the MRS cluster.

-  The NTP service has been installed on the ECS OS and is running properly.

   If the NTP service is not installed, run the **yum install ntp -y** command to install it when the **yum** source is configured.

-  A user can log in to the Linux ECS using the password (in SSH mode).

.. _mrs_01_2127__en-us_topic_0264269828_section181806577218:

Installing a Client on a Node Inside a Cluster
----------------------------------------------

#. Obtain the software package.

   Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Click the name of the cluster to be operated in the **Cluster** drop-down list.

   Choose **More > Download Client**. The **Download Cluster Client** dialog box is displayed.

   .. note::

      In the scenario where only one client is to be installed, choose **Cluster >** **Service >** *Service name* **> More > Download Client**. The **Download Client** dialog box is displayed.

#. Set the client type to **Complete Client**.

   **Configuration Files Only** is to download client configuration files in the following scenario: After a complete client is downloaded and installed and administrators modify server configurations on Manager, developers need to update the configuration files during application development.

   The platform type can be set to **x86_64** or **aarch64**.

   -  **x86_64**: indicates the client software package that can be deployed on the x86 servers.
   -  **aarch64**: indicates the client software package that can be deployed on the TaiShan servers.

   .. note::

      The cluster supports two types of clients: **x86_64** and **aarch64**. The client type must match the architecture of the node for installing the client. Otherwise, client installation will fail.

#. Select **Save to Path** and click **OK** to generate the client file.

   The generated file is stored in the **/tmp/FusionInsight-Client** directory on the active management node by default. You can also store the client file in a directory on which user **omm** has the read, write, and execute permissions. Copy the software package to the file directory on the server where the client is to be installed as user **omm** or **root**.

   The name of the client software package is in the follow format: **FusionInsight_Cluster\_\ <**\ *Cluster ID*\ **>\ \_Services_Client.tar**. In this section, the cluster ID **1** is used as an example. Replace it with the actual cluster ID.

   The following steps and sections use **FusionInsight_Cluster_1_Services_Client.tar** as an example.

   .. note::

      If you cannot obtain the permissions of user **root**, use user **omm**.

      To install the client on another node in the cluster, run the following command to copy the client to the node where the client is to be installed:

      **scp -p /**\ *tmp/FusionInsight-Client*\ **/FusionInsight_Cluster_1_Services_Client.tar** *IP address of the node where the client is to be installed:/opt/Bigdata/client*

#. Log in to the server where the client software package is located as user **user_client**.

#. Decompress the software package.

   Go to the directory where the installation package is stored, such as **/tmp/FusionInsight-Client**. Run the following command to decompress the installation package to a local directory:

   **tar -xvf** **FusionInsight_Cluster_1_Services_Client.tar**

#. Verify the software package.

   Run the following command to verify the decompressed file and check whether the command output is consistent with the information in the **sha256** file.

   **sha256sum -c** **FusionInsight_Cluster_1_Services_ClientConfig.tar.sha256**

   .. code-block::

      FusionInsight_Cluster_1_Services_ClientConfig.tar: OK

#. Decompress the obtained installation file.

   **tar -xvf** **FusionInsight_Cluster_1_Services_ClientConfig.tar**

#. Go to the directory where the installation package is stored, and run the following command to install the client to a specified directory (an absolute path), for example, **/opt/client**:

   **cd /tmp/FusionInsight-Client/FusionInsight\_Cluster_1_Services_ClientConfig**

   Run the **./install.sh /opt/client** command to install the client. The client is successfully installed if information similar to the following is displayed:

   .. code-block::

      The component client is installed successfully

   .. note::

      -  If the clients of all or some services use the **/opt/client** directory, other directories must be used when you install other service clients.
      -  You must delete the client installation directory when uninstalling a client.
      -  To ensure that an installed client can only be used by the installation user (for example, **user_client**), add parameter **-o** during the installation. That is, run the **./install.sh /opt/client -o** command to install the client.
      -  If an HBase client is installed, it is recommended that the client installation directory contain only uppercase and lowercase letters, digits, and characters\ ``(_-?.@+=)`` due to the limitation of the Ruby syntax used by HBase.

Using a Client
--------------

#. On the node where the client is installed, run the **sudo su - omm** command to switch the user. Run the following command to go to the client directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *MRS cluster user*

   Example: **kinit admin**

   .. note::

      User **admin** is created by default for MRS clusters with Kerberos authentication enabled and is used for administrators to maintain the clusters.

#. Run the client command of a component directly.

   For example, run the **hdfs dfs -ls /** command to view files in the HDFS root directory.

Installing a Client on a Node Outside a Cluster
-----------------------------------------------

#. Create an ECS that meets the requirements in :ref:`Prerequisites <mrs_01_2127__en-us_topic_0264269828_en-us_topic_0270713152_en-us_topic_0264269418_section3219221104310>`.
#. Perform NTP time synchronization to synchronize the time of nodes outside the cluster with that of the MRS cluster.

   a. Run the **vi /etc/ntp.conf** command to edit the NTP client configuration file, add the IP addresses of the master node in the MRS cluster, and comment out the IP address of other servers.

      .. code-block::

         server master1_ip prefer
         server master2_ip


      .. figure:: /_static/images/en-us_image_0000001438729629.png
         :alt: **Figure 1** Adding the master node IP addresses

         **Figure 1** Adding the master node IP addresses

   b. Run the **service ntpd stop** command to stop the NTP service.

   c. Run the following command to manually synchronize the time:

      **/usr/sbin/ntpdate** *192.168.10.8*

      .. note::

         **192.168.10.8** indicates the IP address of the active Master node.

   d. Run the **service ntpd start** or **systemctl restart ntpd** command to start the NTP service.

   e. Run the **ntpstat** command to check the time synchronization result.

#. Perform the following steps to download the cluster client software package from FusionInsight Manager, copy the package to the ECS node, and install the client:

   a. Log in to FusionInsight Manager and download the cluster client to the specified directory on the active management node by referring to :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>` and :ref:`Installing a Client on a Node Inside a Cluster <mrs_01_2127__en-us_topic_0264269828_section181806577218>`.

   b. Log in to the active management node as user **root** and run the following command to copy the client installation package to the target node:

      **scp -p /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar** *IP address of the node where the client is to be installed*\ **:/tmp**

   c. Log in to the node on which the client is to be installed as the client user.

      Run the following commands to install the client. If the user does not have operation permissions on the client software package and client installation directory, grant the permissions using the **root** user.

      **cd /tmp**

      **tar -xvf** **FusionInsight_Cluster_1_Services_Client.tar**

      **tar -xvf** **FusionInsight_Cluster_1_Services_ClientConfig.tar**

      **cd FusionInsight\_Cluster_1_Services_ClientConfig**

      **./install.sh /opt/client**

   d. Run the following commands to switch to the client directory and configure environment variables:

      **cd /opt/client**

      **source bigdata_env**

   e. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *MRS cluster user*

      Example: **kinit admin**

   f. Run the client command of a component directly.

      For example, run the **hdfs dfs -ls /** command to view files in the HDFS root directory.
