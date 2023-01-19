:original_name: mrs_01_0800.html

.. _mrs_01_0800:

Using an MRS Client on Nodes Outside a MRS Cluster
==================================================

Scenario
--------

After a client is installed, you can use the client on a node outside an MRS cluster.

Prerequisites
-------------

-  A Linux ECS has been prepared. For details about the OS and its version of the ECS, see :ref:`Table 1 <mrs_01_0800__en-us_topic_0000001237758831_en-us_topic_0270713152_en-us_topic_0264269418_table40818788104630>`.

   .. _mrs_01_0800__en-us_topic_0000001237758831_en-us_topic_0270713152_en-us_topic_0264269418_table40818788104630:

   .. table:: **Table 1** Reference list

      +-------------------------+-----------------------+-------------------------------------------------+
      | CPU Architecture        | Operating System (OS) | Supported Version                               |
      +=========================+=======================+=================================================+
      | x86 computing           | Euler                 | Euler OS 2.5                                    |
      +-------------------------+-----------------------+-------------------------------------------------+
      |                         | SLES                  | SUSE Linux Enterprise Server 12 SP4 (SUSE 12.4) |
      +-------------------------+-----------------------+-------------------------------------------------+
      |                         | RedHat                | Red Hat-7.5-x86_64 (Red Hat 7.5)                |
      +-------------------------+-----------------------+-------------------------------------------------+
      |                         | CentOS                | CentOS-7.6                                      |
      +-------------------------+-----------------------+-------------------------------------------------+
      | Kunpeng computing (Arm) | Euler                 | Euler OS 2.8                                    |
      +-------------------------+-----------------------+-------------------------------------------------+
      |                         | CentOS                | CentOS-7.6                                      |
      +-------------------------+-----------------------+-------------------------------------------------+

   In addition, sufficient disk space is allocated for the ECS, for example, **40GB**.

-  The ECS and the MRS cluster are in the same VPC.

-  The security group of the ECS must be the same as that of the Master node in an MRS cluster.

-  The NTP service has been installed on the ECS OS and is running properly.

   If the NTP service is not installed, run the **yum install ntp -y** command to install it when the **yum** source is configured.

-  A user can log in to the Linux ECS using the password (in SSH mode).

Procedure
---------

#. Create an ECS that meets the requirements.
#. Perform NTP time synchronization to synchronize the time of nodes outside the cluster with the time of the MRS cluster.

   a. Run the **vi /etc/ntp.conf** command to edit the NTP client configuration file, add the IP address of the Master node in the MRS cluster, and comment out the IP addresses of other servers.

      .. code-block::

         server master1_ip profer
         server master2_ip


      .. figure:: /_static/images/en-us_image_0000001389636106.png
         :alt: **Figure 1** Adding the Master node IP addresses

         **Figure 1** Adding the Master node IP addresses

   b. Run the **service ntpd stop** command to stop the NTP service.

   c. Run the **/usr/sbin/ntpdate** *IP address of the active Master node* command to manually synchronize the time.

   d. Run the **service ntpd start** or **systemctl restart ntpd** command to start the NTP service.

   e. Run the **ntpstat** command to check the time synchronization result:

#. Perform the following steps to download the cluster client software package from FusionInsight Manager, copy the package to the ECS node, and install the client:

   a. Log in to FusionInsight Manager and download the cluster client to the specified directory on the active management node.

   b. Log in to the active management node as user **root**.

      **sudo su - omm**

   c. Run the following command to copy the client to the node where the client is to be installed:

      **scp -p /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar** *IP address of the node where the client is to be installed*\ **:/tmp**

   d. Log in to a node on which the client is to be installed as the client user.

      Run the following command to install the client. If you do not have the file operation permission, change the file permission as user **root**.

      **cd /tmp**

      **tar -xvf** **FusionInsight_Cluster_1_Services_Client.tar**

      **tar -xvf** **FusionInsight_Cluster_1_Services_ClientConfig.tar**

      **cd /tmp/FusionInsight\_Cluster_1_Services_ClientConfig**

      **./install.sh /opt/mrsclient**

   e. Run the following commands to switch to the client directory and configure environment variables:

      **cd /opt/mrsclient**

      **source bigdata_env**

   f. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step:

      **kinit** *MRS cluster user*

      Example: **kinit admin**

   g. Run the client command of a component directly.

      For example, run the **hdfs dfs -ls /** command to view files in the HDFS root directory.
