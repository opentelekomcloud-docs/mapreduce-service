:original_name: mrs_01_2128.html

.. _mrs_01_2128:

Installing a Client (Versions Earlier Than 3.x)
===============================================

Scenario
--------

An MRS client is required. The MRS cluster client can be installed on the Master or Core node in the cluster or on a node outside the cluster.

After a cluster of versions earlier than MRS 3.x is created, a client is installed on the active Master node by default. You can directly use the client. The installation directory is **/opt/client**.

For details about how to install a client of MRS 3.x or later, see :ref:`Installing a Client (Version 3.x or Later) <mrs_01_2127>`.

.. note::

   If a client has been installed on the node outside the MRS cluster and the client only needs to be updated, update the client using the user who installed the client, for example, user **root**.

Prerequisites
-------------

-  An ECS has been prepared. For details about the OS and its version of the ECS, see :ref:`Table 1 <mrs_01_2128__en-us_topic_0264269418_table40818788104630>`.

   .. _mrs_01_2128__en-us_topic_0264269418_table40818788104630:

   .. table:: **Table 1** Reference list

      +-----------------------------------+-----------------------------------+
      | OS                                | Supported Version                 |
      +===================================+===================================+
      | EulerOS                           | -  Available: EulerOS 2.2         |
      |                                   | -  Available: EulerOS 2.3         |
      |                                   | -  Available: EulerOS 2.5         |
      +-----------------------------------+-----------------------------------+

   For example, a user can select the enterprise image **Enterprise_SLES11_SP4_latest(4GB)** or standard image **Standard_CentOS_7.2_latest(4GB)** to prepare the OS for an ECS.

   In addition, sufficient disk space is allocated for the ECS, for example, 40 GB.

-  The ECS and the MRS cluster are in the same VPC.

-  The security group of the ECS is the same as that of the Master node of the MRS cluster.

   If this requirement is not met, modify the ECS security group or configure the inbound and outbound rules of the ECS security group to allow the ECS security group to be accessed by all security groups of MRS cluster nodes.

-  To enable users to log in to a Linux ECS using a password (SSH), see **Instances** *>* **Logging In to a Linux ECS** *>* **Login Using an SSH Password** *in the Elastic Cloud Server User Guide*.

Installing a Client on the Core Node
------------------------------------

#. Log in to MRS Manager and choose **Services** > **Download Client** to download the client installation package to the active management node.

   .. note::

      If only the client configuration file needs to be updated, see method 2 in :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_2130>`.

#. Use the IP address to search for the active management node, and log in to the active management node using VNC.

#. Log in to the active management node, and run the following command to switch the user:

   **sudo su - omm**

#. On the MRS management console, view the IP address on the **Nodes** tab page of the specified cluster.

   Record the IP address of the Core node where the client is to be used.

#. On the active management node, run the following command to copy the client installation package to the Core node:

   **scp -p /tmp/MRS-client/MRS\_Services_Client.tar** *IP address of the Core node*\ **:/opt/client**

#. Log in to the Core node as user **root**.

   For details, see `Login Using an SSH Key <https://docs.otc.t-systems.com/usermanual/ecs/en-us_topic_0017955380.html>`__.

#. Run the following commands to install the client:

   **cd /opt/client**

   **tar -xvf** **MRS\_Services_Client.tar**

   **tar -xvf MRS\ \_\ Services_ClientConfig.tar**

   **cd /opt/client/MRS\_Services_ClientConfig**

   **./install.sh** *Client installation directory*

   For example, run the following command:

   **./install.sh /opt/client**

#. For details about how to use the client, see :ref:`Using an MRS Client <mrs_01_2128__en-us_topic_0264269418_section8796733802>`.

.. _mrs_01_2128__en-us_topic_0264269418_section8796733802:

Using an MRS Client
-------------------

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

Installing a Client on a Node Outside the Cluster
-------------------------------------------------

#. Create an ECS that meets the requirements in the prerequisites.

#. .. _mrs_01_2128__en-us_topic_0264269418_li1148114223118:

   Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (Versions Earlier Than MRS 3.x) <mrs_01_0102>`. Then, choose **Services**.

#. Click **Download Client**.

#. In **Client Type**, select **All client files**.

#. In **Download To**, select **Remote host**.

#. .. _mrs_01_2128__en-us_topic_0264269418_li24260068101924:

   Set **Host IP Address** to the IP address of the ECS, **Host Port** to **22**, and **Save Path** to **/home/linux**.

   -  If the default port **22** for logging in to an ECS using SSH has been changed, set **Host Port** to the new port.
   -  **Save Path** contains a maximum of 256 characters.

#. Set **Login User** to **root**.

   If other users are used, ensure that the users have read, write, and execute permission on the save path.

#. In **SSH Private Key**, select and upload the key file used for creating cluster B.

#. Click **OK** to generate a client file.

   If the following information is displayed, the client package is saved. Click **Close**. Obtain the client file from the save path on the remote host that is set when the client is downloaded.

   .. code-block:: text

      Client files downloaded to the remote host successfully.

   If the following information is displayed, check the username, password, and security group configurations of the remote host. Ensure that the username and password are correct and an inbound rule of the SSH (22) port has been added to the security group of the remote host. And then, go to :ref:`2 <mrs_01_2128__en-us_topic_0264269418_li1148114223118>` to download the client again.

   .. code-block:: text

      Failed to connect to the server. Please check the network connection or parameter settings.

   .. note::

      Generating a client will occupy a large number of disk I/Os. You are advised not to download a client when the cluster is being installed, started, and patched, or in other unstable states.

#. Log in to the ECS using VNC. For details, see **Instance** > **Logging In to a Linux** > **Logging In to a Linux** in the *Elastic Cloud Server* *User Guide*

   Log in to the ECS. For details, see `Login Using an SSH Key <https://docs.otc.t-systems.com/usermanual/ecs/en-us_topic_0017955380.html>`__. Set the ECS password and log in to the ECS in VNC mode.

#. Perform NTP time synchronization to synchronize the time of nodes outside the cluster with the time of the MRS cluster.

   a. Check whether the NTP service is installed. If it is not installed, run the **yum install ntp -y** command to install it.

   b. Run the **vim /etc/ntp.conf** command to edit the NTP client configuration file, add the IP address of the Master node in the MRS cluster, and comment out the IP addresses of other servers.

      .. code-block::

         server master1_ip prefer
         server master2_ip


      .. figure:: /_static/images/en-us_image_0000001388250740.png
         :alt: **Figure 1** Adding the Master node IP addresses

         **Figure 1** Adding the Master node IP addresses

   c. Run the **service ntpd stop** command to stop the NTP service.

   d. Run the following command to manually synchronize the time:

      **/usr/sbin/ntpdate** *192.168.10.8*

      .. note::

         **192.168.10.8** indicates the IP address of the active Master node.

   e. Run the **service ntpd start** or **systemctl restart ntpd** command to start the NTP service.

   f. Run the **ntpstat** command to check the time synchronization result:

#. On the ECS, switch to user **root** and copy the installation package in **Save Path** in :ref:`6 <mrs_01_2128__en-us_topic_0264269418_li24260068101924>` to the **/opt** directory. For example, if **Save Path** is set to **/home/linux**, run the following commands:

   **sudo su - root**

   **cp /home/linux/MRS_Services_Client.tar /opt**

#. Run the following command in the **/opt** directory to decompress the package and obtain the verification file and the configuration package of the client:

   **tar -xvf MRS\_Services_Client.tar**

#. Run the following command to verify the configuration file package of the client:

   **sha256sum -c MRS\_Services_ClientConfig.tar.sha256**

   The command output is as follows:

   .. code-block::

      MRS_Services_ClientConfig.tar: OK

#. Run the following command to decompress **MRS_Services_ClientConfig.tar**:

   **tar -xvf MRS\_Services_ClientConfig.tar**

#. Run the following command to install the client to a new directory, for example, **/opt/Bigdata/client**. A directory is automatically generated during the client installation.

   **sh /opt/MRS\_Services_ClientConfig/install.sh /opt/Bigdata/client**

   If the following information is displayed, the client has been successfully installed:

   .. code-block::

      Components client installation is complete.

#. Check whether the IP address of the ECS node is connected to the IP address of the cluster Master node.

   For example, run the following command: **ping** *Master node IP address*.

   -  If yes, go to :ref:`18 <mrs_01_2128__en-us_topic_0264269418_li6406429718107>`.
   -  If no, check whether the VPC and security group are correct and whether the ECS and the MRS cluster are in the same VPC and security group, and go to :ref:`18 <mrs_01_2128__en-us_topic_0264269418_li6406429718107>`.

#. .. _mrs_01_2128__en-us_topic_0264269418_li6406429718107:

   Run the following command to configure environment variables:

   **source /opt/Bigdata/client/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *MRS cluster user*

   Example: **kinit admin**

#. Run the client command of a component.

   For example, run the following command to query the HDFS directory:

   **hdfs dfs -ls /**
