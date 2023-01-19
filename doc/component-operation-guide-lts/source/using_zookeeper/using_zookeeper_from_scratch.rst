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

#. Download the client configuration file.

   a. Log in to FusionInsight Manager. For details, see. :ref:`Accessing FusionInsight Manager <mrs_01_2124>`

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
