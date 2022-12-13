:original_name: mrs_01_1595.html

.. _mrs_01_1595:

Installing the Flume Client on MRS 3.\ *x* or Later Clusters
============================================================

Scenario
--------

To use Flume to collect logs, you must install the Flume client on a log host. You can create an ECS and install the Flume client on it.

This section applies to MRS 3.\ *x* or later clusters.

Prerequisites
-------------

-  A cluster with the Flume component has been created.
-  The log host is in the same VPC and subnet with the MRS cluster.
-  You have obtained the username and password for logging in to the log host.
-  The installation directory is automatically created if it does not exist. If it exists, the directory must be left blank. The directory path cannot contain any space.

Procedure
---------

#. Obtain the software package.

   Log in to the FusionInsight Manager. Choose **Cluster** > *Name of the target cluster* > **Services** > **Flume**. On the Flume service page that is displayed, choose **More** > **Download Client** in the upper right corner and set **Select Client Type** to **Complete Client** to download the Flume service client file.

   The file name of the client is **FusionInsight_Cluster\_**\ <*Cluster ID*>\ **\_Flume_Client.tar**. This section takes the client file **FusionInsight_Cluster_1_Flume_Client.tar** as an example.

#. Upload the software package.

   Upload the software package to a directory, for example, **/opt/client** on the node where the Flume service client will be installed as user **user**.

   .. note::

      **user** is the user who installs and runs the Flume client.

#. Decompress the software package.

   Log in to the node where the Flume service client is to be installed as user **user**. Go to the directory where the installation package is installed, for example, **/opt/client**, and run the following command to decompress the installation package to the current directory:

   **cd /opt/client**

   **tar -xvf FusionInsight\_Cluster_1_Flume_Client.tar**

#. Verify the software package.

   Run the **sha256sum -c** command to verify the decompressed file. If **OK** is returned, the verification is successful. Example:

   **sha256sum -c FusionInsight\_Cluster_1_Flume_ClientConfig.tar.sha256**

   .. code-block::

      FusionInsight_Cluster_1_Flume_ClientConfig.tar: OK

#. Decompress the package.

   **tar -xvf FusionInsight\_Cluster_1_Flume_ClientConfig.tar**

#. Run the following command in the Flume client installation directory to install the client to a specified directory (for example, **opt/FlumeClient**): After the client is installed successfully, the installation is complete.

   **cd /opt/client/FusionInsight\_Cluster_1_Flume_ClientConfig/Flume/FlumeClient**

   **./install.sh -d /**\ *opt/FlumeClient* **-f** *MonitorServerService IP address or host name of the role* **-c** *User service configuration filePath for storing properties.properties* **-s** *CPU threshold* **-l /var/log/Bigdata -e** *FlumeServer service IP address or host name* **-n** *Flume*

   .. note::

      -  **-d**: Flume client installation path

      -  (Optional) **-f**: IP addresses or host names of two MonitorServer roles. The IP addresses or host names are separated by commas (,). If this parameter is not configured, the Flume client does not send alarm information to MonitorServer and information about the client cannot be viewed on the FusionInsight Manager GUI.

      -  (Optional) **-c**: Service configuration file, which needs to be generated on the configuration tool page of the Flume server based on your service requirements. Upload the file to any directory on the node where the client is to be installed. If this parameter is not specified during the installation, you can upload the generated service configuration file **properties.properties** to the **/opt/FlumeClient/fusioninsight-flume-1.9.0/conf** directory after the installation.

      -  (Optional) **-s**: cgroup threshold. The value is an integer ranging from 1 to 100 x *N*. *N* indicates the number of CPU cores. The default threshold is **-1**, indicating that the processes added to the cgroup are not restricted by the CPU usage.

      -  (Optional) **-l**: Log path. The default value is **/var/log/Bigdata**. The user **user** must have the write permission on the directory. When the client is installed for the first time, a subdirectory named **flume-client** is generated. After the installation, subdirectories named **flume-client-**\ *n* will be generated in sequence. The letter *n* indicates a sequence number, which starts from 1 in ascending order. In the **/conf/** directory of the Flume client installation directory, modify the **ENV_VARS** file and search for the **FLUME_LOG_DIR** attribute to view the client log path.

      -  (Optional) **-e**: Service IP address or host name of FlumeServer, which is used to receive statistics for the monitoring indicator reported by the client.

      -  (Optional) **-n**: Name of the Flume client. You can choose **Cluster** > *Name of the desired cluster* > **Service** > **Flume** > **Flume Management** on FusionInsight Manager to view the client name on the corresponding node.

      -  If the following error message is displayed, run the **export JAVA_HOME=\ JDK path** command.

         .. code-block::

            JAVA_HOME is null in current user,please install the JDK and set the JAVA_HOME

      -  IBM JDK does not support **-Xloggc**. You must change **-Xloggc** to **-Xverbosegclog** in **flume/conf/flume-env.sh**. For 32-bit JDK, the value of **-Xmx** must not exceed 3.25 GB.

      -  When installing a cross-platform client in a cluster, go to the **/opt/client/FusionInsight_Cluster_1_Flume_ClientConfig/Flume/FusionInsight-Flume-1.9.0.tar.gz** directory to install the Flume client.
