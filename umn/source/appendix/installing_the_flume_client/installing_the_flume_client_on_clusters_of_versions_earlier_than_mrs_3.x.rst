:original_name: mrs_01_1594.html

.. _mrs_01_1594:

Installing the Flume Client on Clusters of Versions Earlier Than MRS 3.x
========================================================================

Scenario
--------

To use Flume to collect logs, you must install the Flume client on a log host. You can create an ECS and install the Flume client on it.

This section applies to MRS 3.\ *x* or earlier clusters.

Prerequisites
-------------

-  A streaming cluster with the Flume component has been created.
-  The log host is in the same VPC and subnet with the MRS cluster.
-  You have obtained the username and password for logging in to the log host.

Procedure
---------

#. Create an ECS that meets the requirements.

#. Go to the cluster details page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components**.

#. .. _mrs_01_1594__en-us_topic_0265836944_li1514145518420:

   Click **Download Client**.

   a. In **Client Type**, select **All client files**.

   b. In **Download to**, select **Remote host**.

   c. Set **Host IP Address** to the IP address of the ECS, **Host Port** to **22**, and **Save Path** to **/home/linux**.

      -  If the default port **22** for logging in to an ECS through SSH has been changed, set **Host Port** to a new port.
      -  The value of **Save Path** contains a maximum of 256 characters.

   d. Set **Login User** to **root**.

      If another user is used, ensure that the user has permissions to read, write, and execute the save path.

   e. In **SSH Private Key**, select and upload the key file used for creating the cluster.

   f. Click **OK** to generate a client file.

      If the following information is displayed, the client package is saved.

      .. code-block:: text

         Client files downloaded to the remote host successfully.

      If the following information is displayed, check the username, password, and security group configurations of the remote host. Ensure that the username and password are correct and an inbound rule of the SSH (22) port has been added to the security group of the remote host. And then, go to :ref:`3 <mrs_01_1594__en-us_topic_0265836944_li1514145518420>` to download the client again.

      .. code-block:: text

         Failed to connect to the server. Please check the network connection or parameter settings.

#. Choose **Flume** > **Instance**. Query the **Business IP Address** of any Flume instance and any two MonitorServer instances.

#. Log in to the ECS using VNC. See section "Login Using VNC" in the *Elastic Cloud Service User Guide* (**Instances** > **Logging In to a Linux ECS** > **Login Using VNC**.

   Log in to the ECS using an SSH key by referring to `Login Using an SSH Key <https://docs.otc.t-systems.com/usermanual/ecs/en-us_topic_0017955380.html>`__ and set the password. Then log in to the ECS using VNC.

#. On the ECS, switch to user **root** and copy the installation package to the **/opt** directory.

   **sudo su - root**

   **cp /home/linux/MRS_Flume_Client.tar /opt**

#. Run the following command in the **/opt** directory to decompress the package and obtain the verification file and the configuration package of the client:

   **tar -xvf MRS_Flume_Client.tar**

#. Run the following command to verify the configuration package of the client:

   **sha256sum -c MRS_Flume_ClientConfig.tar.sha256**

   If the following information is displayed, the file package is successfully verified:

   .. code-block::

      MRS_Flume_ClientConfig.tar: OK

#. Run the following command to decompress **MRS_Flume_ClientConfig.tar**:

   **tar -xvf MRS_Flume_ClientConfig.tar**

#. Run the following command to install the client running environment to a new directory, for example, **/opt/Flumeenv**. A directory is automatically generated during the client installation.

   **sh /opt/MRS_Flume_ClientConfig/install.sh /opt/Flumeenv**

   If the following information is displayed, the client running environment is successfully installed:

   .. code-block::

      Components client installation is complete.

#. Run the following command to configure environment variables:

   **source /opt/Flumeenv/bigdata_env**

#. Run the following commands to decompress the Flume client package:

   **cd /opt/MRS_Flume_ClientConfig/Flume**

   **tar -xvf FusionInsight-Flume-1.6.0.tar.gz**

#. Run the following command to check whether the password of the current user has expired:

   **chage -l root**

   If the value of **Password expires** is earlier than the current time, the password has expired. Run the **chage -M -1 root** command to validate the password.

#. Run the following command to install the Flume client to a new directory, for example, **/opt/FlumeClient**. A directory is automatically generated during the client installation.

   **sh /opt/MRS_Flume_ClientConfig/Flume/install.sh -d /opt/FlumeClient -f** *service IP address of the MonitorServer instance* **-c** *path of the Flume configuration file* **-l /var/log/ -e** *service IP address of Flume* **-n** *name of the Flume client*

   The parameters are described as follows:

   -  **-d**: indicates the installation path of the Flume client.
   -  (Optional) **-f**: indicates the service IP addresses of the two MonitorServer instances, separated by a comma (,). If the IP addresses are not configured, the Flume client will not send alarm information to MonitorServer, and the client information will not be displayed on MRS Manager.
   -  (Optional) **-c**: indicates the **properties.properties** configuration file that the Flume client loads after installation. If this parameter is not specified, the **fusioninsight-flume-1.6.0/conf/properties.properties** file in the client installation directory is used by default. The configuration file of the client is empty. You can modify the configuration file as required and the Flume client will load it automatically.
   -  (Optional) **-l**: indicates the log directory. The default value is **/var/log/Bigdata**.
   -  (Optional) **-e**: indicates the service IP address of the Flume instance. It is used to receive the monitoring indicators reported by the client.
   -  (Optional) **-n**: indicates the name of the Flume client.
   -  IBM JDK does not support **-Xloggc**. You must change **-Xloggc** to **-Xverbosegclog** in **flume/conf/flume-env.sh**. For 32-bit JDK, the value of **-Xmx** must not exceed 3.25 GB.
   -  In **flume/conf/flume-env.sh**, the default value of **-Xmx** is 4 GB. If the client memory is too small, you can change it to 512 MB or even 1 GB.

   For example, run **sh install.sh -d /opt/FlumeClient**.

   If the following information is displayed, the client is successfully installed:

   .. code-block::

      install flume client successfully.
