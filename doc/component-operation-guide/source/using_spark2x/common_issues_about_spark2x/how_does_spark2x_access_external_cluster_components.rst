:original_name: mrs_01_2062.html

.. _mrs_01_2062:

How Does Spark2x Access External Cluster Components?
====================================================

Question
--------

There are two clusters, cluster 1 and cluster 2. How do I use Spark2x in cluster 1 to access HDFS, Hive, HBase, and Kafka components in cluster 2?

Answer
------

#. Components in two clusters can access each other. However, there are the following restrictions:

   -  Only one Hive MetaStore can be accessed. Specifically, Hive MetaStore in cluster 1 and Hive MetaStore in cluster 2 cannot be accessed at the same time.
   -  User systems in different clusters are not synchronized. When users access components in another cluster, user permission is determined by the user configuration of the peer cluster. For example, if user A of cluster 1 does not have the permissions to access the HBase meta table in cluster 1 but user A of cluster 2 can access the HBase meta table in cluster 2, user A of cluster 1 can access the HBase meta table in cluster 2.
   -  To enable components in a security cluster to communicate with each other across Manager, you need to configure mutual trust.

#. The following describes how to access Hive, HBase, and Kafka components in cluster 2 as user A.

   .. note::

      The following operations are based on the scenario where a user uses the FusionInsight client to submit the Spark2x application. If the user uses the configuration file directory, the user needs to modify the corresponding file in the configuration directory of the application and upload the configuration file to the executor.

      When the HDFS and HBase clients access the server, **hostname** is used to configure the server address. Therefore, the hosts configuration of all nodes to be accessed must be saved in the **/etc/hosts** file on the client. You can add the host of the peer cluster node to the **/etc/hosts** file of the client node in advance.

   -  Access Hive metastore: Replace the **hive-site.xml** file in the **conf** directory of the Spark2x client in cluster 1 with the **hive-site.xml** file in the **conf** directory of the Spark2x client in cluster 2.

      After the preceding operations are performed, you can use Spark SQL to access Hive MetaStore. To access Hive table data, you need to perform the operations in :ref:`• Access HDFS of two clusters at the same time: <mrs_01_2062__li13277182417246>` and set **nameservice** of the peer cluster to **LOCATION**.

   -  Access HBase of the peer cluster.

      a. Configure the IP addresses and host names of all ZooKeeper nodes and HBase nodes in cluster 2 in the **/etc/hosts** file on the client node of cluster 1.
      b. Replace the **hbase-site.xml** file in the **conf** directory of the Spark2x client in cluster 1 with the **hbase-site.xml** file in the **conf** directory of the Spark2x client in cluster 2.

   -  Access Kafka: Set the address of the Kafka Broker to be accessed to the Kafka Broker address in cluster 2.

   -  .. _mrs_01_2062__li13277182417246:

      Access HDFS of two clusters at the same time:

      -  Two tokens with the same NameService cannot be obtained at the same time. Therefore, the NameServices of the HDFS in two clusters must be different. For example, one is **hacluster**, and the other is **test**.

         a. Obtain the following configurations from the **hdfs-site.xml** file of cluster2 and add them to the **hdfs-site.xml** file in the **conf** directory of the Spark2x client in cluster1:

            **dfs.nameservices.mappings**, **dfs.nameservices**, **dfs.namenode.rpc-address.test.\***, **dfs.ha.namenodes.test**, and **dfs.client.failover.proxy.provider.test**

            The following is an example:

            .. code-block::

               <property>
               <name>dfs.nameservices.mappings</name>
               <value>[{"name":"hacluster","roleInstances":["14","15"]},{"name":"test","roleInstances":["16","17"]}]</value>
               </property>
               <property>
               <name>dfs.nameservices</name>
               <value>hacluster,test</value>
               </property>
               <property>
               <name>dfs.namenode.rpc-address.test.16</name>
               <value>192.168.0.1:8020</value>
               </property>
               <property>
               <name>dfs.namenode.rpc-address.test.17</name>
               <value>192.168.0.2:8020</value>
               </property>
               <property>
               <name>dfs.ha.namenodes.test</name>
               <value>16,17</value>
               </property>
               <property>
               <name>dfs.client.failover.proxy.provider.test</name>
               <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
               </property>

         b. Modify **spark.yarn.extra.hadoopFileSystems = hdfs://test and spark.hadoop.hdfs.externalToken.enable = true** in the **spark-defaults.conf** configuration file under the **conf** directory on the Spark client of cluster 1.

            .. code-block::

               spark.yarn.extra.hadoopFileSystems = hdfs://test
               spark.hadoop.hdfs.externalToken.enable = true

         c. In the application submission command, add the **--keytab** and **--principal** parameters and set them to the user who submits the task in cluster1.
         d. Use the Spark client of cluster1 to submit the application. Then, the two HDFS services can be accessed at the same time.

   -  Access HBase of two clusters at the same time:

      a. Modify **spark.hadoop.hbase.externalToken.enable = true** in the **spark-defaults.conf** configuration file under the **conf** directory on the Spark client of cluster 1.

         .. code-block::

            spark.hadoop.hbase.externalToken.enable = true

      b. When accessing HBase, you need to use the configuration file of the corresponding cluster to create a **Configuration** object for creating a **Connection** object.

      c. In an MRS cluster, tokens of multiple HBase services can be obtained at the same time to solve the problem that the executor cannot access HBase. The method is as follows:

         Assume that you need to access HBase of the current cluster and HBase of cluster2. Save the **hbase-site.xml** file of cluster2 in a compressed package named **external_hbase_conf**\***, and use **--archives** to specify the compressed package when submitting the command.
