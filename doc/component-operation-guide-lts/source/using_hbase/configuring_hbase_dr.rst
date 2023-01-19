:original_name: mrs_01_1609.html

.. _mrs_01_1609:

Configuring HBase DR
====================

Scenario
--------

HBase disaster recovery (DR), a key feature that is used to ensure high availability (HA) of the HBase cluster system, provides the real-time remote DR function for HBase. HBase DR provides basic O&M tools, including tools for maintaining and re-establishing DR relationships, verifying data, and querying data synchronization progress. To implement real-time DR, back up data of an HBase cluster to another HBase cluster. DR in the HBase table common data writing and BulkLoad batch data writing scenarios is supported.

Prerequisites
-------------

-  The active and standby clusters are successfully installed and started, and you have the administrator permissions on the clusters.

-  Ensure that the network connection between the active and standby clusters is normal and ports are available.
-  If the active cluster is deployed in security mode and is not managed by one FusionInsight Manager, cross-cluster trust relationship has been configured for the active and standby clusters.. If the active cluster is deployed in normal mode, no cross-cluster mutual trust is required.
-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Copy <mrs_01_0502>`.
-  Time is consistent between the active and standby clusters and the NTP service on the active and standby clusters uses the same time source.
-  Mapping relationships between the names of all hosts in the active and standby clusters and IP addresses have been configured in the hosts files of all the nodes in the active and standby clusters and of the node where the active cluster client resides.
-  The network bandwidth between the active and standby clusters is determined based on service volume, which cannot be less than the possible maximum service volume.
-  The MRS versions of the active and standby clusters must be the same.
-  The scale of the standby cluster must be greater than or equal to that of the active cluster.

Constraints
-----------

-  Although DR provides the real-time data replication function, the data synchronization progress is affected by many factors, such as the service volume in the active cluster and the health status of the standby cluster. In normal cases, the standby cluster should not take over services. In extreme cases, system maintenance personnel and other decision makers determine whether the standby cluster takes over services according to the current data synchronization indicators.

-  HBase clusters must be deployed in active/standby mode.
-  Table-level operations on the DR table of the standby cluster are forbidden, such as modifying the table attributes and deleting the table. Misoperations on the standby cluster will cause data synchronization failure of the active cluster. As a result, table data in the standby cluster is lost.
-  If the DR data synchronization function is enabled for HBase tables of the active cluster, the DR table structure of the standby cluster needs to be modified to ensure table structure consistency between the active and standby clusters during table structure modification.

Procedure
---------

**Configuring the common data writing DR parameters for the active cluster**

#. Log in to Manager of the active cluster.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations** and click **All Configurations**. The HBase configuration page is displayed.

#. (Optional) :ref:`Table 1 <mrs_01_1609__en-us_topic_0000001173949368_tcc2ebdc7794f4718bf8175f779496069>` describes the optional configuration items during HBase DR. You can set the parameters based on the description or use the default values.

   .. _mrs_01_1609__en-us_topic_0000001173949368_tcc2ebdc7794f4718bf8175f779496069:

   .. table:: **Table 1** Optional configuration items

      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Navigation Path            | Parameter                                    | Default Value | Description                                                                                                                                                                                                                                                                                                                                             |
      +============================+==============================================+===============+=========================================================================================================================================================================================================================================================================================================================================================+
      | HMaster > Performance      | hbase.master.logcleaner.ttl                  | 600000        | Specifies the retention period of HLog. If the value is set to **604800000** (unit: millisecond), the retention period of HLog is 7 days.                                                                                                                                                                                                               |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                            | hbase.master.cleaner.interval                | 60000         | Interval for the HMaster to delete historical HLog files. The HLog that exceeds the configured period will be automatically deleted. You are advised to set it to the maximum value to save more HLogs.                                                                                                                                                 |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | RegionServer > Replication | replication.source.size.capacity             | 16777216      | Maximum size of edits, in bytes. If the edit size exceeds the value, HLog edits will be sent to the standby cluster.                                                                                                                                                                                                                                    |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                            | replication.source.nb.capacity               | 25000         | Maximum number of edits, which is another condition for triggering HLog edits to be sent to the standby cluster. After data in the active cluster is synchronized to the standby cluster, the active cluster reads and sends data in HLog according to this parameter value. This parameter is used together with **replication.source.size.capacity**. |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                            | replication.source.maxretriesmultiplier      | 10            | Maximum number of retries when an exception occurs during replication.                                                                                                                                                                                                                                                                                  |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                            | replication.source.sleepforretries           | 1000          | Retry interval (Unit: ms)                                                                                                                                                                                                                                                                                                                               |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                            | hbase.regionserver.replication.handler.count | 6             | Number of replication RPC server instances on RegionServer                                                                                                                                                                                                                                                                                              |
      +----------------------------+----------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Configuring the BulkLoad batch data writing DR parameters for the active cluster**

4. Determine whether to enable the BulkLoad batch data writing DR function.

   If yes, go to :ref:`5 <mrs_01_1609__en-us_topic_0000001173949368_l4716d1d3802e4b24ba3b3b49cf396866>`.

   If no, go to :ref:`8 <mrs_01_1609__en-us_topic_0000001173949368_l3a38ddf2af1b455995b7223d0fe94c23>`.

5. .. _mrs_01_1609__en-us_topic_0000001173949368_l4716d1d3802e4b24ba3b3b49cf396866:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations** and click **All Configurations**. The HBase configuration page is displayed.

6. Search for **hbase.replication.bulkload.enabled** and change its value to **true** to enable the BulkLoad batch data writing DR function.

7. Search for **hbase.replication.cluster.id** and change the HBase ID of the active cluster. The ID is used by the standby cluster to connect to the active cluster. The value can contain uppercase letters, lowercase letters, digits, and underscores (_), and cannot exceed 30 characters.

**Restarting the HBase service and install the client**

8. .. _mrs_01_1609__en-us_topic_0000001173949368_l3a38ddf2af1b455995b7223d0fe94c23:

   Click **Save**. In the displayed dialog box, click **OK**. Restart the HBase service.

9. In the active and standby clusters, choose **Cluster >** **Name of the desired cluster** **> Service > HBase > More > Download Client** to download the client and install it.

**Adding the DR relationship between the active and standby clusters**

10. Log in as user **hbase** to the HBase shell page of the active cluster.

11. Run the following command on HBase Shell to create the DR synchronization relationship between the active cluster HBase and the standby cluster HBase.

    **add_peer '**\ *Standby cluster ID*\ **', CLUSTER_KEY => "**\ *ZooKeeper service IP address in the standby cluster* **", CONFIG => {"hbase.regionserver.kerberos.principal" => "**\ *Standby cluster RegionServer principal*\ **", "hbase.master.kerberos.principal" => "**\ *Standby cluster HMaster principal*\ **"}**

    -  The standby cluster ID indicates the ID for the active cluster to recognize the standby cluster. Enter an ID. The value can be specified randomly. Digits are recommended.
    -  The ZooKeeper address of the standby cluster includes the service IP address of ZooKeeper, the port for listening to client connections, and the HBase root directory of the standby cluster on ZooKeeper.
    -  Search for **hbase.master.kerberos.principal** and **hbase.regionserver.kerberos.principal** in the HBase **hbase-site.xml** configuration file of the standby cluster.

    For example, to add the DR relationship between the active and standby clusters, run the **add_peer '**\ *Standby cluster ID*\ **', CLUSTER_KEY => "192.168.40.2,192.168.40.3,192.168.40.4:24002:/hbase", CONFIG => {"hbase.regionserver.kerberos.principal" => "hbase/hadoop.hadoop.com@HADOOP.COM", "hbase.master.kerberos.principal" => "hbase/hadoop.hadoop.com@HADOOP.COM"}**

12. (Optional) If the BulkLoad batch data write DR function is enabled, the HBase client configuration of the active cluster must be copied to the standby cluster.

    -  Create the **/hbase/replicationConf/**\ **hbase.replication.cluster.id of the active cluster** directory in the HDFS of the standby cluster.

    -  HBase client configuration file, which is copied to the **/hbase/replicationConf/hbase.replication.cluster.id of the active cluster** directory of the HDFS of the standby cluster.

       Example: **hdfs dfs -put HBase/hbase/conf/core-site.xml HBase/hbase/conf/hdfs-site.xml HBase/hbase/conf/yarn-site.xml hdfs://NameNode IP:25000/hbase/replicationConf/source_cluster**

**Enabling HBase DR to synchronize data**

13. Check whether a naming space exists in the HBase service instance of the standby cluster and the naming space has the same name as the naming space of the HBase table for which the DR function is to be enabled.

    -  If the same namespace exists, go to :ref:`14 <mrs_01_1609__en-us_topic_0000001173949368_li254519151517>`.
    -  If no, create a naming space with the same name in the HBase shell of the standby cluster and go to :ref:`14 <mrs_01_1609__en-us_topic_0000001173949368_li254519151517>`.

14. .. _mrs_01_1609__en-us_topic_0000001173949368_li254519151517:

    In the HBase shell of the active cluster, run the following command as user **hbase** to enable the real-time DR function for the table data of the active cluster to ensure that the data modified in the active cluster can be synchronized to the standby cluster in real time.

    You can only synchronize the data of one HTable at a time.

    **enable_table_replication '**\ *table name*\ **'**

    .. note::

       -  If the standby cluster does not contain a table with the same name as the table for which real-time synchronization is to be enabled, the table is automatically created.
       -  If a table with the same name as the table for which real-time synchronization is to be enabled exists in the standby cluster, the structures of the two tables must be the same.
       -  If the encryption algorithm SMS4 or AES is configured for '*Table name*', the function for synchronizing data from the active cluster to the standby cluster cannot be enabled for the HBase table.
       -  If the standby cluster is offline or has tables with the same name but different structures, the DR function cannot be enabled.
       -  If the DR data synchronization function is enabled for some Phoenix tables in the active cluster, the standby cluster cannot have common HBase tables with the same names as the Phoenix tables in the active cluster. Otherwise, the DR function fails to be enabled or the tables with the names in the standby cluster cannot be used properly.
       -  If the DR data synchronization function is enabled for Phoenix tables in the active cluster, you need to enable the DR data synchronization function for the metadata tables of the Phoenix tables. The metadata tables include SYSTEM.CATALOG, SYSTEM.FUNCTION, SYSTEM.SEQUENCE, and SYSTEM.STATS.
       -  If the DR data synchronization function is enabled for HBase tables of the active cluster, after adding new indexes to HBase tables, you need to manually add secondary indexes to DR tables in the standby cluster to ensure secondary index consistency between the active and standby clusters.

15. (Optional) If HBase does not use Ranger, run the following command as user **hbase** in the HBase shell of the active cluster to enable the real-time permission to control data DR function for the HBase tables in the active cluster.

    **enable_table_replication 'hbase:acl'**

**Creating Users**

16. Log in to FusionInsight Manager of the standby cluster, choose **System** > **Permission** > **Role** > **Create Role** to create a role, and add the same permission for the standby data table to the role based on the permission of the HBase source data table of the active cluster.
17. Choose **System** > **Permission** > **User** > **Create** to create a user. Set the **User Type** to **Human-Machine** or **Machine-Machine** based on service requirements and add the user to the created role. Access the HBase DR data of the standby cluster as the newly created user.

    .. note::

       -  After the permission of the active HBase source data table is modified, to ensure that the standby cluster can properly read data, modify the role permission for the standby cluster.
       -  If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for HBase <mrs_01_1857>`.

**Synchronizing the table data of the active cluster**

18. After HBase DR is configured and data synchronization is enabled, check whether tables and data exist in the active cluster and whether the historical data needs to be synchronized to the standby cluster.

    -  If yes, a table exists and data needs to be synchronized. Log in as the HBase table user to the node where the HBase client of the active cluster is installed and run the kinit username to authenticate the identity. The user must have the read and write permissions on tables and the execute permission on the **hbase:meta** table. Then go to :ref:`19 <mrs_01_1609__en-us_topic_0000001173949368_li2511113725912>`.
    -  If no, no further action is required.

19. .. _mrs_01_1609__en-us_topic_0000001173949368_li2511113725912:

    The HBase DR configuration does not support automatic synchronization of historical data in tables. You need to back up the historical data of the active cluster and then manually restore the historical data in the standby cluster.

    Manual recovery refers to the recovery of a single table, which can be performed through Export, DistCp, or Import.

    To manually recover a single table, perform the following steps:

    a. Export table data from the active cluster.

       **hbase org.apache.hadoop.hbase.mapreduce.Export -Dhbase.mapreduce.include.deleted.rows=true** *Table name* *Directory where the source data is stored*

       Example: **hbase org.apache.hadoop.hbase.mapreduce.Export -Dhbase.mapreduce.include.deleted.rows=true t1 /user/hbase/t1**

    b. Copy the data that has been exported to the standby cluster.

       **hadoop distcp** *directory where the source data is stored on the active cluster* **hdfs://**\ *ActiveNameNodeIP:8020/directory where the source data is stored on the standby cluster*

       **ActiveNameNodeIP** indicates the IP address of the active NameNode in the standby cluster.

       Example: **hadoop distcp /user/hbase/t1 hdfs://192.168.40.2:8020/user/hbase/t1**

    c. Import data to the standby cluster as the HBase table user of the standby cluster.

       On the HBase shell screen of the standby cluster, run the following command as user **hbase** to retain the data writing status:

       **set_clusterState_active**

       The command is run successfully if the following information is displayed:

       .. code-block::

          hbase(main):001:0> set_clusterState_active
          => true

       **hbase org.apache.hadoop.hbase.mapreduce.Import** *-Dimport.bulk.output=Directory where the output data is stored in the standby cluster Table name Directory where the source data is stored in the standby cluster*

       **hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles** *Directory where the output data is stored in the standby cluster Table name*

       Example:

       .. code-block::

          hbase(main):001:0> set_clusterState_active
          => true

       **hbase org.apache.hadoop.hbase.mapreduce.Import -Dimport.bulk.output=/user/hbase/output_t1 t1 /user/hbase/t1**

       **hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /user/hbase/output_t1 t1**

20. Run the following command on the HBase client to check the synchronized data of the active and standby clusters. After the DR data synchronization function is enabled, you can run this command to check whether the newly synchronized data is consistent.

    **hbase org.apache.hadoop.hbase.mapreduce.replication.VerifyReplication --starttime**\ *=Start time* **--endtime**\ *=End time* *Column family name ID of the standby cluster Table name*

    .. note::

       -  The start time must be earlier than the end time.
       -  The values of **starttime** and **endtime** must be in the timestamp format. You need to run **date -d "2015-09-30 00:00:00" +%s to** change a common time format to a timestamp format.

**Specify the data writing status for the active and standby clusters.**

21. On the HBase shell screen of the active cluster, run the following command as user **hbase** to retain the data writing status:

    **set_clusterState_active**

    The command is run successfully if the following information is displayed:

    .. code-block::

       hbase(main):001:0> set_clusterState_active
       => true

22. On the HBase shell screen of the standby cluster, run the following command as user **hbase** to retain the data read-only status:

    **set_clusterState_standby**

    The command is run successfully if the following information is displayed:

    .. code-block::

       hbase(main):001:0> set_clusterState_standby
       => true

Related Commands
----------------

.. table:: **Table 2** HBase DR

   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                                                                       | Command                                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                                                                           |
   +=================================================================================+================================================================================================================================================================================================================================================================================+=======================================================================================================================================================================================================================================================================================================================+
   | Set up a DR relationship.                                                       | add_peer'*Standby cluster ID*', CLUSTER_KEY => "*Standby cluster ZooKeeper service IP address*", CONFIG => {"hbase.regionserver.kerberos.principal" => "*Standby cluster RegionServer principal*", "hbase.master.kerberos.principal" => "*Standby cluster HMaster principal*"} | Set up the relationship between the active cluster and the standby cluster.                                                                                                                                                                                                                                           |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | **add_peer '1','zk1,zk2,zk3:2181:/hbase1'**                                                                                                                                                                                                                                    | If BulkLoad batch data write DR is enabled:                                                                                                                                                                                                                                                                           |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | 2181: port number of ZooKeeper in the cluster                                                                                                                                                                                                                                  | -  Create the **/hbase/replicationConf/hbase.replication.cluster.id of the active cluster** directory in the HDFS of the standby cluster.                                                                                                                                                                             |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  HBase client configuration file, which is copied to the **/hbase/replicationConf/hbase.replication.cluster.id of the active cluster** directory of the HDFS of the standby cluster.                                                                                                                                |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Remove the DR relationship.                                                     | **remove_peer** *'Standby cluster ID'*                                                                                                                                                                                                                                         | Remove standby cluster information from the active cluster.                                                                                                                                                                                                                                                           |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | Example:                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | **remove_peer '1'**                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                       |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Querying the DR Relationship                                                    | **list_peers**                                                                                                                                                                                                                                                                 | Query standby cluster information (mainly Zookeeper information) in the active cluster.                                                                                                                                                                                                                               |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Enable the real-time user table synchronization function.                       | **enable_table_replication** *'Table name'*                                                                                                                                                                                                                                    | Synchronize user tables from the active cluster to the standby cluster.                                                                                                                                                                                                                                               |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | Example:                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | **enable_table_replication 't1'**                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                       |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Disable the real-time user table synchronization function.                      | **disable_table_replication** *'Table name'*                                                                                                                                                                                                                                   | Do not synchronize user tables from the active cluster to the standby cluster.                                                                                                                                                                                                                                        |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | Example:                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | **disable_table_replication 't1'**                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                       |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Verify data of the active and standby clusters.                                 | **bin/hbase org.apache.hadoop.hbase.mapreduce.replication.VerifyReplication --starttime=**\ *Start time* **--endtime=**\ *End time* *Column family name Standby cluster ID Table name*                                                                                         | Verify whether data of the specified table is the same between the active cluster and the standby cluster.                                                                                                                                                                                                            |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | The description of the parameters in this command is as follows:                                                                                                                                                                                                                                                      |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  Start time: If start time is not specified, the default value **0** will be used.                                                                                                                                                                                                                                  |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  End time: If end time is not specified, the time when the current operation is submitted will be used by default.                                                                                                                                                                                                  |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  Table name: If a table name is not entered, all user tables for which the real-time synchronization function is enabled will be verified by default.                                                                                                                                                               |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Switch the data writing status.                                                 | **set_clusterState_active**                                                                                                                                                                                                                                                    | Specifies whether data can be written to the cluster HBase tables.                                                                                                                                                                                                                                                    |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 | **set_clusterState_standby**                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                       |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Add or update the active cluster HDFS configurations saved in the peer cluster. | **hdfs dfs -put -f HBase/hbase/conf/core-site.xml HBase/hbase/conf/hdfs-site.xml HBase/hbase/conf/yarn-site.xml hdfs://**\ *Standby cluster* **NameNode** **IP:PORT/hbase/replicationConf/**\ *Active cluster*\ **hbase.replication.cluster.id**                               | Enable DR for data including bulkload data. When HDFS parameters are modified in the active cluster, the modification cannot be automatically synchronized from the active cluster to the standby cluster. You need to manually run the command to synchronize configuration. The affected parameters are as follows: |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  fs.defaultFS                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  dfs.client.failover.proxy.provider.hacluster                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  dfs.client.failover.connection.retries.on.timeouts                                                                                                                                                                                                                                                                 |
   |                                                                                 |                                                                                                                                                                                                                                                                                | -  dfs.client.failover.connection.retries                                                                                                                                                                                                                                                                             |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | For example, change **fs.defaultFS** to **hdfs://hacluster_sale**,                                                                                                                                                                                                                                                    |
   |                                                                                 |                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                       |
   |                                                                                 |                                                                                                                                                                                                                                                                                | HBase client configuration file, which is copied to the **/hbase/replicationConf/hbase.replication.cluster.id of the active cluster** directory of the HDFS of the standby cluster.                                                                                                                                   |
   +---------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
