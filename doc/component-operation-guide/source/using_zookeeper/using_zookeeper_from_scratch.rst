:original_name: mrs_01_2093.html

.. _mrs_01_2093:

Using ZooKeeper from Scratch
============================

ZooKeeper is an open-source, highly reliable, and distributed consistency coordination service. ZooKeeper is designed to solve the problem that data consistency cannot be ensured for complex and error-prone distributed systems. There is no need to develop dedicated collaborative applications, which is suitable for high availability services to ensure data consistency.

Background Information
----------------------

Before using the client, you need to download and update the client configuration file on all clients except the client of the active management node.

Procedure
---------

For MRS 2.\ *x* or earlier, perform the following operations:

#. .. _mrs_01_2093__l6b58a848ef0f4fe6a361d4ef0ac39fb8:

   Download the client configuration file.

   a. Log in to the MRS console. In the left navigation pane, choose **Clusters** > **Active Clusters**, and click the cluster to be operated.

   b. Click the **Components** tab.

   c. Click **Services** and then **Download Client**.

      Set **Client Type** to **Only configuration files**, and click **OK** to generate the client configuration file. The generated file is saved in the **/tmp/MRS-client** directory on the active management node by default. You can customize the file path.

#. Log in to the active management node of MRS Manager.

   a. On the MRS console, choose **Clusters > Active Clusters** and click a cluster name. On the **Nodes** tab, view the node names. The node whose name contains **master1** is the Master1 node, and the node whose name contains **master2** is the Master2 node.

      The active and standby management nodes of MRS Manager are installed on Master nodes by default. Because Master1 and Master2 are switched over in active and standby mode, Master1 is not always the active management node of MRS Manager. Run a command in Master1 to check whether Master1 is active management node of MRS Manager. For details about the command, see :ref:`2.d <mrs_01_2093__le8e7045cece741e8b6209b929a50ff22>`.

   b. Log in to the Master1 node using the password as user **root**.

   c. Run the following commands to switch to user **omm**:

      **sudo su - root**

      **su - omm**

   d. .. _mrs_01_2093__le8e7045cece741e8b6209b929a50ff22:

      Run the following command to check the active management node of MRS Manager:

      **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh**

      In the command output, the node whose **HAActive** is **active** is the active management node, and the node whose **HAActive** is **standby** is the standby management node. In the following example, **mgtomsdat-sh-3-01-1** is the active management node, and **mgtomsdat-sh-3-01-2** is the standby management node.

      .. code-block::

         Ha mode
         double
         NodeName              HostName                      HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
         192-168-0-30          mgtomsdat-sh-3-01-1           V100R001C01        2014-11-18 23:43:02      active               normal               Actived
         192-168-0-24          mgtomsdat-sh-3-01-2           V100R001C01        2014-11-21 07:14:02      standby              normal               Deactived

   e. Log in to the active management node, for example, **192-168-0-30** of MRS Manager as user **root**, and run the following command to switch to user **omm**:

      **sudo su - omm**

#. Run the following command to go to the client installation directory, for example, **/opt/client**.

   **cd /opt/client**

#. .. _mrs_01_2093__li15639738131312:

   Run the following command to update the client configuration for the active management node.

   **sh refreshConfig.sh /opt/client** *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/client/tmp/MRS-client/MRS_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully:

   .. code-block::

       ReFresh components client config is complete.
       Succeed to refresh components client config.

   .. note::

      You can perform :ref:`1 <mrs_01_2093__l6b58a848ef0f4fe6a361d4ef0ac39fb8>` to :ref:`4 <mrs_01_2093__li15639738131312>` by referring to Method 2 in :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_2130>` .

#. Use the client on a Master node.

   a. On the active management node where the client is updated, for example, node **192-168-0-30**, run the following command to go to the client directory:

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step:

      **kinit** *MRS cluster user*

      Example: **kinit zookeeperuser**.

   d. Run the following Zookeeper client command:

      **zkCli.sh -server** *<zookeeper installation node IP>*\ **:<port>**

      Example: **zkCli.sh -server node-master1DGhZ:2181**

#. Run the ZooKeeper client command.

   a. Create a ZNode.

      .. code-block::

         create /test

   b. View ZNode information.

      .. code-block::

         ls /

   c. Write data to the ZNode.

      .. code-block::

         set /test "zookeeper test"

   d. View the data written to the ZNode.

      .. code-block::

         get /test

   e. Delete the created ZNode.

      .. code-block::

         delete /test

For MRS 3.x or later, perform the following operations:

#. Download the client configuration file.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Dashboard** > **More** > **Download Client**.

   c. Download the cluster client.

      Set **Select Client Type** to **Configuration Files Only**, select a platform type, and click **OK** to generate the client configuration file which is then saved in the **/tmp/FusionInsight-Client/** directory on the active management node by default.

#. Log in to the active management node of Manager.

   a. Log in to any node where Manager is deployed as user **root**.

   b. Run the following command to identify the active and standby nodes:

      **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh**

      In the command output, the value of **HAActive** for the active management node is **active**, and that for the standby management node is **standby**. In the following example, **node-master1** is the active management node, and **node-master2** is the standby management node.

      .. code-block::

         HAMode
         double
         NodeName             HostName        HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
         192-168-0-30         node-master1    V100R001C01        2020-05-01 23:43:02      active               normal               Actived
         192-168-0-24         node-master2    V100R001C01        2020-05-01 07:14:02      standby              normal               Deactived

   c. Log in to the primary management node as user **root** and run the following command to switch to user **omm**:

      **sudo su - omm**

#. Run the following command to go to the client installation directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to update the client configuration for the active management node.

   **sh refreshConfig.sh /opt/client** *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/client /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully:

   .. code-block::

      ReFresh components client config is complete.
      Succeed to refresh components client config.

5. Use the client on a Master node.

   a. On the active management node where the client is updated, for example, node **192-168-0-30**, run the following command to go to the client directory:

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication has been enabled for the current cluster, run the following command to authenticate the current user. If Kerberos authentication is disabled for the current cluster, skip this step:

      **kinit** *MRS cluster user*

      Example: **kinit zookeeperuser**.

   d. Run the following Zookeeper client command:

      *zkCli.sh -server <zookeeper installation node IP>:<port>*

      Example: **zkCli.sh -server node-master1DGhZ:2181**

6. Run the ZooKeeper client command.

   a. Create a ZNode.

      .. code-block::

         create /test

   b. View ZNode information.

      .. code-block::

         ls /

   c. Write data to the ZNode.

      .. code-block::

         set /test "zookeeper test"

   d. View the data written to the ZNode.

      .. code-block::

         get /test

   e. Delete the created ZNode.

      .. code-block::

         delete /test
