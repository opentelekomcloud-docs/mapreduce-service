:original_name: mrs_03_1196.html

.. _mrs_03_1196:

How Do I Modify the HDFS Active/Standby Switchover Class?
=========================================================

If the **org.apache.hadoop.hdfs.server.namenode.ha.AdaptiveFailoverProxyProvider** class is unavailable when a cluster of MRS 3.\ *x* connects to NameNodes using HDFS, the cause is that the HDFS active/standby switchover class of the cluster is configured improperly. To solve the problem, perform the following operations:

-  Method 1: Add the **hadoop-plugins-xxx.jar** package to the **classpath** or **lib** directory of your program.

   The **hadoop-plugins-xxx.jar** package is stored in the HDFS client directory, for example, **$HADOOP_HOME/share/hadoop/common/lib/hadoop-plugins-8.0.2-302023.jar**.

-  Method 2: Change the configuration item of HDFS to the corresponding open source class, as shown in the follows:

   dfs.client.failover.proxy.provider.hacluster=org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider
