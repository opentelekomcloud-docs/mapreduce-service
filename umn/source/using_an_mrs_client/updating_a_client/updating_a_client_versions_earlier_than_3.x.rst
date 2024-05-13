:original_name: mrs_01_0089.html

.. _mrs_01_0089:

Updating a Client (Versions Earlier Than 3.x)
=============================================

.. note::

   This section applies to clusters of versions earlier than MRS 3.x. For MRS 3.x or later, see :ref:`Updating a Client (Version 3.x or Later) <mrs_01_24209>`.

Updating a Client Configuration File
------------------------------------

**Scenario**

An MRS cluster provides a client for you to connect to a server, view task results, or manage data. Before using an MRS client, you need to download and update the client configuration file if service configuration parameters are modified and a service is restarted or the service is merely restarted on MRS Manager.

During cluster creation, the original client is stored in the **/opt/client** directory on all nodes in the cluster by default. After the cluster is created, only the client of a Master node can be directly used. To use the client of a Core node, you need to update the client configuration file first.

**Procedure**

**Method 1:**

#. Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`. Then, choose **Services**.

#. Click **Download Client**.

   Set **Client Type** to **Only configuration files**, **Download To** to **Server**, and click **OK** to generate the client configuration file. The generated file is saved in the **/tmp/MRS-client** directory on the active management node by default. You can customize the file path.

#. Query and log in to the active Master node.

#. If you use the client in the cluster, run the following command to switch to user **omm**. If you use the client outside the cluster, switch to user **root**.

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/Bigdata/client**:

   **cd /opt/Bigdata/client**

#. Run the following command to update client configurations:

   **sh refreshConfig.sh** *Client installation directory* *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/Bigdata/client /tmp/MRS-client/MRS_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      ReFresh components client config is complete.
      Succeed to refresh components client config.

**Method 2: applicable to MRS 1.9.2 or later**

#. After the cluster is installed, run the following command to switch to user **omm**. If you use the client outside the cluster, switch to user **root**.

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/Bigdata/client**:

   **cd /opt/Bigdata/client**

#. Run the following command and enter the name of an MRS Manager user with the download permission and its password (for example, the username is **admin** and the password is the one set during cluster creation) as prompted to update client configurations.

   **sh autoRefreshConfig.sh**

#. After the command is executed, the following information is displayed, where *XXX* indicates the name of the component installed in the cluster. To update client configurations of all components, press **Enter**. To update client configurations of some components, enter the component names and separate them with commas (,).

   .. code-block::

      Components "xxx" have been installed in the cluster. Please input the comma-separated names of the components for which you want to update client configurations. If you press Enter without inputting any component name, the client configurations of all components will be updated:

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      Succeed to refresh components client config.

   If the following information is displayed, the username or password is incorrect.

   .. code-block::

      login manager failed,Incorrect username or password.

   .. note::

      -  This script automatically connects to the cluster and invokes the **refreshConfig.sh** script to download and update the client configuration file.
      -  By default, the client uses the floating IP address specified by **wsom=xxx** in the **Version** file in the installation directory to update the client configurations. To update the configuration file of another cluster, modify the value of **wsom=xxx** in the **Version** file to the floating IP address of the corresponding cluster before performing this step.

Fully Updating the Original Client of the Active Master Node
------------------------------------------------------------

**Scenario**

During cluster creation, the original client is stored in the **/opt/client** directory on all nodes in the cluster by default. The following uses **/opt/Bigdata/client** as an example.

-  For a normal MRS cluster, you will use the pre-installed client on a Master node to submit a job on the management console page.
-  You can also use the pre-installed client on the Master node to connect to a server, view task results, and manage data.

After installing the patch on the cluster, you need to update the client on the Master node to ensure that the functions of the built-in client are available.

**Procedure**

#. .. _mrs_01_0089__li6500547131416:

   Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`. Then, choose **Services**.

#. Click **Download Client**.

   Set **Client Type** to **All client files**, **Download To** to **Server**, and click **OK** to generate the client configuration file. The generated file is saved in the **/tmp/MRS-client** directory on the active management node by default. You can customize the file path.

#. .. _mrs_01_0089__li14850170195112:

   Query and log in to the active Master node.

#. .. _mrs_01_0089__li3635762195625:

   On the ECS, switch to user **root** and copy the installation package to the **/opt** directory.

   **sudo su - root**

   **cp /tmp/MRS-client/MRS_Services_Client.tar /opt**

#. Run the following command in the **/opt** directory to decompress the package and obtain the verification file and the configuration package of the client:

   **tar -xvf MRS\_Services_Client.tar**

#. Run the following command to verify the configuration file package of the client:

   **sha256sum -c MRS\_Services_ClientConfig.tar.sha256**

   The command output is as follows:

   .. code-block::

      MRS_Services_ClientConfig.tar: OK

#. Run the following command to decompress **MRS_Services_ClientConfig.tar**:

   **tar -xvf MRS\_Services_ClientConfig.tar**

#. Run the following command to move the original client to the **/opt/Bigdata/client_bak** directory:

   **mv /opt/Bigdata/client** **/opt/Bigdata/client_bak**

#. Run the following command to install the client in a new directory. The client path must be **/opt/Bigdata/client**.

   **sh /opt/MRS\_Services_ClientConfig/install.sh /opt/Bigdata/client**

   If the following information is displayed, the client has been successfully installed:

   .. code-block::

      Components client installation is complete.

#. Run the following command to modify the user and user group of the **/opt/Bigdata/client** directory:

   **chown omm:wheel /opt/Bigdata/client -R**

#. Run the following command to configure environment variables:

   **source /opt/Bigdata/client/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *MRS cluster user*

   Example: **kinit admin**

#. .. _mrs_01_0089__li6221236418107:

   Run the client command of a component.

   For example, run the following command to query the HDFS directory:

   **hdfs dfs -ls /**

Fully Updating the Original Client of the Standby Master Node
-------------------------------------------------------------

#. Repeat :ref:`1 <mrs_01_0089__li6500547131416>` to :ref:`3 <mrs_01_0089__li14850170195112>` to log in to the standby Master node, and run the following command to switch to user **omm**:

   **sudo su - omm**

#. Run the following command on the standby master node to copy the downloaded client package from the active master node:

   **scp omm@**\ *master1 nodeIP address*\ **:/tmp/MRS-client/MRS_Services_Client.tar /tmp/MRS-client/**

   .. note::

      -  In this command, **master1** node is the active master node.
      -  **/tmp/MRS-client/** is an example target directory of the standby master node.

#. Repeat :ref:`4 <mrs_01_0089__li3635762195625>` to :ref:`13 <mrs_01_0089__li6221236418107>` to update the client of the standby Master node.
