:original_name: admin_guide_000171.html

.. _admin_guide_000171:

Installing a Client
===================

Scenario
--------

This section describes how to install the clients of all services, except Flume, in the MRS cluster. MRS provides shell scripts for different services so that maintenance personnel can log in to related maintenance clients and implement maintenance operations.

.. note::

   -  Reinstall the client after server configuration is modified on FusionInsight Manager or after the system is upgraded. Otherwise, the versions of the client and server will be inconsistent.

Prerequisites
-------------

-  An installation directory will be automatically created if it does not exist. If the directory exists, it must be empty. The directory cannot contain any space.
-  If a server outside the cluster is used as the client node, the node can communicate with the cluster service plane. Otherwise, client installation will fail.
-  The client must have the NTP service enabled and synchronized time with the NTP server. Otherwise, client installation will fail.
-  If clients of all components are downloaded, HDFS and MapReduce are installed in the same directory (*Client directory*\ **/HDFS/**).
-  You can install and use the client as any user whose username and password have been obtained from the system administrator. This section uses **user_client** as an example. Ensure that user **user_client** is the owner of the server file directory (for example, **/opt/Bigdata/hadoopclient**) and client installation directory (for example, **/opt/client**). The permission for the two directories is **755**.
-  You have obtained the component service username (a default user or new user) and password from the system administrator.
-  When you install the client as a user other than **omm** or **root**, and the **/var/tmp/patch** directory already exists, you have changed the permission for the directory to **777** and changed the permission for the logs in the directory to **666**.

Procedure
---------

#. Obtain the required software packages.

   Log in to FusionInsight Manager. Click the wanted cluster from the **Cluster** drop-down list.

   Click **More** and select **Download Client**. The **Download Cluster Client** page is displayed.

   .. note::

      If only one component client is to be installed, choose **Cluster**, click the name of the target cluster, choose **Services**, click a service name, click **More**, and select **Download Client**. The **Download Client** page is displayed.

#. Set **Select Client Type** to **Complete Client**.

   **Configuration Files Only** is to download client configuration files in the following scenario: After a complete client is downloaded and installed and the system administrator modifies server configurations on Manager, developers need to update the configuration files during application development.

   The platform type can be set to **x86_64** or **aarch64**.

   -  **x86_64**: indicates the client software package that can be deployed on the x86 servers.
   -  **aarch64**: indicates the client software package that can be deployed on the TaiShan servers.

   .. note::

      The cluster supports two types of clients: **x86_64** and **aarch64**. The client type must match the architecture of the node for installing the client. Otherwise, client installation will fail.

#. Determine whether to generate a client file on the cluster node.

   -  If yes, select **Save to Path**, and click **OK** to generate the client file. By default, the client file is generated in **/tmp/FusionInsight-Client** on the active management node. You can also store the client file in other directories, and user **omm** has the read, write, and execute permissions on the directories. Copy the software package to the file directory, for example, **/opt/Bigdata/hadoopclient**, on the server where the client is to be installed as user **omm** or **root**. Then, go to :ref:`5 <admin_guide_000171__en-us_topic_0193213980_en-us_topic_0046662333_u_login>`.

      .. note::

         If you cannot obtain the permissions of user **root**, use user **omm**.

   -  If no, click **OK** and specify a local save path to download the complete client. Wait until the download is complete and go to :ref:`4 <admin_guide_000171__en-us_topic_0193213980_li4528442311580>`.

#. .. _admin_guide_000171__en-us_topic_0193213980_li4528442311580:

   Upload the software package.

   Use WinSCP to upload the obtained software package as the user (such as **user_client**) who prepares for the installation, to the directory (such as **/opt/Bigdata/hadoopclient**) of the server where the client is to be installed.

   The name of the client software package is in the follow format: **FusionInsight_Cluster\_\ <**\ *Cluster ID*\ **>\ \_Services_Client.tar**.

   The following steps and sections use **FusionInsight_Cluster_1_Services_Client.tar** as an example.

   .. note::

      The host where the client is to be installed can be a node inside or outside the cluster. If the node is a server outside the cluster, it must be able to communicate with the cluster, and the NTP service must be enabled to ensure that the time is the same as that on the server.

      For example, you can configure the same NTP clock source for external servers as that of the cluster. After the configuration, you can run the **ntpq -np** command to check whether the time is synchronized.

      -  If there is an asterisk (*) before the IP address of the NTP clock source in the command output, the synchronization is normal. For example:

         .. code-block::

            remote refid st t when poll reach delay offset jitter
            ==============================================================================
            *10.10.10.162 .LOCL. 1 u 1 16 377 0.270 -1.562 0.014

      -  If there is no asterisk (*) before the IP address of the NTP clock source and the value of **refid** is **.INIT.**, or if the command output is abnormal, the synchronization is abnormal. Contact technical support.

         .. code-block::

            remote refid st t when poll reach delay offset jitter
            ==============================================================================
            10.10.10.162 .INIT. 1 u 1 16 377 0.270 -1.562 0.014

      You can also configure the same chrony clock source for external servers as that for the cluster. After the configuration, run the **chronyc sources** command to check whether the time is synchronized.

      -  In the command output, if there is an asterisk (*) before the IP address of the chrony service on the active OMS node, the synchronization is normal. For example:

         .. code-block::

            MS Name/IP address         Stratum Poll Reach LastRx Last sample
            ===============================================================================
            ^* 10.10.10.162             10  10   377   626    +16us[  +15us] +/-  308us

      -  In the command output, if there is no asterisk (*) before the IP address of the NTP service on the active OMS node, and the value of **Reach** is **0**, the synchronization is abnormal.

         .. code-block::

            MS Name/IP address         Stratum Poll Reach LastRx Last sample
            ===============================================================================
            ^? 10.1.1.1                      0  10     0     -     +0ns[   +0ns] +/-    0ns

#. .. _admin_guide_000171__en-us_topic_0193213980_en-us_topic_0046662333_u_login:

   Log in as user **user_client** to the server where the client is to be installed.

#. Decompress the software package.

   Go to the directory where the installation package is stored, for example, **/opt/Bigdata/hadoopclient**. Run the following command to decompress the installation package to a local directory:

   **tar -xvf** **FusionInsight_Cluster_1_Services_Client.tar**

#. Verify the software package.

   Run the following command to verify the decompressed file and check whether the command output is consistent with the information in the **sha256** file:

   **sha256sum -c** **FusionInsight_Cluster_1_Services_ClientConfig.tar.sha256**

   .. code-block::

      FusionInsight_Cluster_1_Services_ClientConfig.tar: OK

#. Decompress the obtained installation file.

   **tar -xvf** **FusionInsight_Cluster_1_Services_ClientConfig.tar**

#. Configure network connections for the client.

   a. Ensure that the host where the client is installed can communicate with the hosts listed in the **hosts** file in the decompression directory (for example, **/opt/Bigdata/hadoopclient/FusionInsight_Cluster\_**\ *<Cluster ID>*\ **\_Services_ClientConfig/hosts**).
   b. If the host where the client is installed is not a host in the cluster, you need to set the mapping between the host name and the service plane IP address for each cluster node in **/etc/hosts**, as user **root**. Each host name uniquely maps an IP address. You can perform the following steps to import the domain name mapping of the cluster to the **hosts** file:

      #. Switch to user **root** or a user who has the permission to modify the **hosts** file.

         **su - root**

      #. Go to the directory where the client package is decompressed.

         **cd /opt/Bigdata/hadoopclient/FusionInsight\_Cluster_1_Services_ClientConfig**

      #. Run the **cat realm.ini >> /etc/hosts** command to import the domain name mapping to the **hosts** file.

   .. note::

      -  If the host where the client is installed is not a node in the cluster, configure network connections for the client to prevent errors when you run commands on the client.
      -  If Spark tasks are executed in yarn-client mode, add the **spark.driver.host** parameter to the file *Client installation directory*\ **/Spark/spark/conf/spark-defaults.conf** and set the parameter to the client IP address.
      -  If the yarn-client mode is used, you need to configure the mapping between the IP address and host name of the client in the **hosts** file on the active and standby Yarn nodes (ResourceManager nodes in the cluster) to make sure that the Spark web UI is properly displayed.

#. Go to the directory where the installation package is stored, and run the following command to install the client to a specified directory (an absolute path), for example, **/opt/client**:

   **cd /opt/Bigdata/hadoopclient/FusionInsight\_Cluster_1_Services_ClientConfig**

   Run the **./install.sh /opt/client** command to install the client. The client is successfully installed if information similar to the following is displayed:

   .. code-block::

      The component client is installed successfully

   .. note::

      -  If the **/opt/hadoopclient** directory has been used by existing service clients, you need to use another directory in this step when installing other service clients.
      -  You must delete the client installation directory when uninstalling a client.
      -  To ensure that an installed client can only be used by the installation user (for example, **user_client**), add parameter **-o** during the installation. That is, run the **./install.sh /opt/hadoopclient -o** command to install the client.
      -  If the NTP server is to be installed in **chrony** mode, ensure that the parameter **chrony** is added during the installation, that is, run the **./install.sh /opt/client -o** **chrony** command to install the client.
      -  If an HBase client is installed, it is recommended that the client installation directory contain only uppercase and lowercase letters, digits, and special characters ``(_-?.@+=)`` due to the limitation of the Ruby syntax used by HBase.
      -  If the client node is a server outside the cluster and cannot communicate with the service plane IP address of the active OMS node or cannot access port 20029 of the active OMS node, the client can be successfully installed but cannot be registered with the cluster or displayed on the UI.

#. Log in to the client to check whether the client is successfully installed.

   a. Run the **cd /opt/client** command to go to the client installation directory.

   b. Run the **source bigdata_env** command to configure environment variables for the client.

   c. For a cluster in security mode, run the following command to set **kinit** authentication and enter the password for logging in to the client. For a cluster in normal mode, user authentication is not required.

      **kinit admin**

      .. code-block::

         Password for xxx@HADOOP.COM: #Enter the login password of user admin (same as the user password for logging in to the cluster).

   d. Run the **klist** command to query and confirm authentication details.

      .. code-block::

         Ticket cache: FILE:/tmp/krb5cc_0
         Default principal: xxx@HADOOP.COM

         Valid starting       Expires              Service principal
         04/09/2021 18:22:35  04/10/2021 18:22:29  krbtgt/HADOOP.COM@HADOOP.COM

      .. note::

         -  When kinit authentication is used, the ticket is stored in the **/tmp/krb5cc\_**\ *uid* directory by default.

            *uid* indicates the ID of the user who logs in to the OS. For example, if the UID of user **root** is 0, the ticket generated for kinit authentication after user **root** logs in to the system is stored in the **/tmp/krb5cc_0** directory.

            If the current user does not have the read/write permission for the **/tmp** directory, the ticket cache path is changed to **Client installation directory/tmp/krb5cc_uid**. For example, if the client installation directory is **/opt/hadoopclient**, the kinit authentication ticket is stored in **/opt/hadoopclient/tmp/krb5cc_uid**.

         -  If the same user is used to log in to the OS for kinit authentication, there is a risk that tickets are overwritten. You can set the **-c** *cache_name* parameter to specify the ticket cache path or set the **KRB5CCNAME** environment variable to avoid this problem.

#. After the cluster is reinstalled, the previously installed client is no longer available. Perform the following operations to deploy the client again:

   a. Log in to the node where the client is deployed as user **root**.

   b. Run the following command to view the directory where the client is located: (In the following example, **/opt/hadoopclient** is the directory where the client is located.)

      **ll /opt**

      .. code-block::

         drwxr-x---. 6 root root       4096 Dec 11 19:00 hadoopclient
         drwxr-xr-x. 3 root root       4096 Dec  9 02:04 godi
         drwx------. 2 root root      16384 Nov  6 01:03 lost+found
         drwxr-xr-x. 2 root root       4096 Nov  7 09:49 rh

   c. Run the following command to delete the files in the folder (for example, **/opt/client**) where all client programs are located:

      **mv /opt/client** */tmp/clientbackup*

   d. Reinstall the client.
