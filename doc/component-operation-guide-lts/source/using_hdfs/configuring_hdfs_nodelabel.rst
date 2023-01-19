:original_name: mrs_01_1676.html

.. _mrs_01_1676:

Configuring HDFS NodeLabel
==========================

Scenario
--------

You need to configure the nodes for storing HDFS file data blocks based on data features. You can configure a label expression to an HDFS directory or file and assign one or more labels to a DataNode so that file data blocks can be stored on specified DataNodes.

If the label-based data block placement policy is used for selecting DataNodes to store the specified files, the DataNode range is specified based on the label expression. Then proper nodes are selected from the specified range.

-  Scenario 1: DataNodes partitioning scenario

   Scenario description:

   When different application data is required to run on different nodes for separate management, label expressions can be used to achieve separation of different services, storing specified services on corresponding nodes.

   By configuring the NodeLabel feature, you can perform the following operations:

   -  Store data in **/HBase** to DN1, DN2, DN3, and DN4.
   -  Store data in **/Spark** to DN5, DN6, DN7, and DN8.

   .. _mrs_01_1676__en-us_topic_0000001219029801_f29094c7c7de94c108e1f8ddea541eab7:

   .. figure:: /_static/images/en-us_image_0000001349259201.png
      :alt: **Figure 1** DataNode partitioning scenario

      **Figure 1** DataNode partitioning scenario

   .. note::

      -  Run the **hdfs nodelabel -setLabelExpression -expression 'LabelA[fallback=NONE]' -path /Hbase** command to set an expression for the **Hbase** directory. As shown in :ref:`Figure 1 <mrs_01_1676__en-us_topic_0000001219029801_f29094c7c7de94c108e1f8ddea541eab7>`, the data block replicas of files in the **/Hbase** directory are placed on the nodes labeled with the **LabelA**, that is, DN1, DN2, DN3, and DN4. Similarly, run the **hdfs nodelabel -setLabelExpression -expression 'LabelB[fallback=NONE]' -path /Spark** command to set an expression for the Spark directory. Data block replicas of files in the **/Spark** directory can be placed only on nodes labeled with **LabelB**, that is, DN5, DN6, DN7, and DN8.
      -  For details about how to set labels for a data node, see :ref:`Configuration Description <mrs_01_1676__en-us_topic_0000001219029801_s7752fba8102e4f20ae2c86f564e2114c>`.
      -  If multiple racks are available in one cluster, it is recommended that DataNodes of these racks should be available under each label, to ensure reliability of data block placement.

-  Scenario 2: Specifying replica location when there are multiple racks

   Scenario description:

   In a heterogeneous cluster, customers need to allocate certain nodes with high availability to store important commercial data. Label expressions can be used to specify replica location so that the replica can be placed on a high reliable node.

   Data blocks in the **/data** directory have three replicas by default. In this case, at least one replica is stored on a node of RACK1 or RACK2 (nodes of RACK1 and RACK2 are high reliable), and the other two are stored separately on the nodes of RACK3 and RACK4.


   .. figure:: /_static/images/en-us_image_0000001349059745.png
      :alt: **Figure 2** Scenario example

      **Figure 2** Scenario example

   .. note::

      Run the **hdfs nodelabel -setLabelExpression -expression 'LabelA||LabelB[fallback=NONE],LabelC,LabelD' -path /data** command to set an expression for the **/data** directory.

      When data is to be written to the **/data** directory, at least one data block replica is stored on a node labeled with the LabelA or LabelB, and the other two data block replicas are stored separately on the nodes labeled with the LabelC and LabelD.

.. _mrs_01_1676__en-us_topic_0000001219029801_s7752fba8102e4f20ae2c86f564e2114c:

Configuration Description
-------------------------

-  DataNode label configuration

   Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. table:: **Table 1** Parameter description

      +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
      | Parameter                      | Description                                                                                                                                                                                                                                                                                                                                                                                              | Default Value                                                                    |
      +================================+==========================================================================================================================================================================================================================================================================================================================================================================================================+==================================================================================+
      | dfs.block.replicator.classname | Used to configure the DataNode policy of HDFS.                                                                                                                                                                                                                                                                                                                                                           | org.apache.hadoop.hdfs.server.blockmanagement.AvailableSpaceBlockPlacementPolicy |
      |                                |                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                  |
      |                                | To enable the NodeLabel function, set this parameter to **org.apache.hadoop.hdfs.server.blockmanagement.BlockPlacementPolicyWithNodeLabel**.                                                                                                                                                                                                                                                             |                                                                                  |
      +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
      | host2tags                      | Used to configure a mapping between a DataNode host and a label.                                                                                                                                                                                                                                                                                                                                         | ``-``                                                                            |
      |                                |                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                  |
      |                                | The host name can be configured with an IP address extension expression (for example, **192.168.1.[1-128]** or **192.168.[2-3].[1-128]**) or a regular expression (for example, **/datanode-[123]/** or **/datanode-\\d{2}/**) starting and ending with a slash (/). The label configuration name cannot contain the following characters: = / \\ **Note**: The IP address must be a service IP address. |                                                                                  |
      +--------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

   .. note::

      -  The **host2tags** configuration item is described as follows:

         Assume there are 20 DataNodes which range from dn-1 to dn-20 in a cluster and the IP addresses of clusters range from 10.1.120.1 to 10.1.120.20. The value of **host2tags** can be represented in either of the following methods:

         **Regular expression of the host name**

         **/dn-\\d/ = label-1** indicates that the labels corresponding to dn-1 to dn-9 are label-1, that is, dn-1 = label-1, dn-2 = label-1, ..., dn-9 = label-1.

         **/dn-((1[0-9]$)|(20$))/ = label-2** indicates that the labels corresponding to dn-10 to dn-20 are label-2, that is, dn-10 = label-2, dn-11 = label-2, ...dn-20 = label-2.

         **IP address range expression**

         **10.1.120.[1-9] = label-1** indicates that the labels corresponding to 10.1.120.1 to 10.1.120.9 are label-1, that is, 10.1.120.1 = label-1, 10.1.120.2 = label-1, ..., and 10.1.120.9 = label-1.

         **10.1.120.[10-20] = label-2** indicates that the labels corresponding to 10.1.120.10 to 10.1.120.20 are label-2, that is, 10.1.120.10 = label-2, 10.1.120.11 = label-2, ..., and 10.1.120.20 = label-2.

      -  Label-based data block placement policies are applicable to capacity expansion and reduction scenarios.

         A newly added DataNode will be assigned a label if the IP address of the DataNode is within the IP address range in the **host2tags** configuration item or the host name of the DataNode matches the host name regular expression in the **host2tags** configuration item.

         For example, the value of **host2tags** is **10.1.120.[1-9] = label-1**, but the current cluster has only three DataNodes: 10.1.120.1 to 10.1.120.3. If DataNode 10.1.120.4 is added for capacity expansion, the DataNode is labeled as label-1. If the 10.1.120.3 DataNode is deleted or out of the service, no data block will be allocated to the node.

-  Set label expressions for directories or files.

   -  On the HDFS parameter configuration page, configure **path2expression** to configure the mapping between HDFS directories and labels. If the configured HDFS directory does not exist, the configuration can succeed. When a directory with the same name as the HDFS directory is created manually, the configured label mapping relationship will be inherited by the directory within 30 minutes. After a labeled directory is deleted, a new directory with the same name as the deleted one will inherit its mapping within 30 minutes.
   -  For details about configuring items using commands, see the **hdfs nodelabel -setLabelExpression** command.
   -  To set label expressions using the Java API, invoke the **setLabelExpression(String src, String labelExpression)** method using the instantiated object NodeLabelFileSystem. *src* indicates a directory or file path on HDFS, and **labelExpression** indicates the label expression.

-  After the NodeLabel is enabled, you can run the **hdfs nodelabel -listNodeLabels** command to view the label information of each DataNode.

Block Replica Location Selection
--------------------------------

Nodelabel supports different placement policies for replicas. The expression **label-1,label-2,label-3** indicates that three replicas are respectively placed in DataNodes containing label-1, label-2, and label-3. Different replica policies are separated by commas (,).

If you want to place two replicas in DataNode with label-1, set the expression as follows: **label-1[replica=2],label-2,label-3**. In this case, if the default number of replicas is 3, two nodes with label-1 and one node with label-2 are selected. If the default number of replicas is 4, two nodes with label-1, one node with label-2, and one node with label-3 are selected. Note that the number of replicas is the same as that of each replica policy from left to right. However, the number of replicas sometimes exceeds the expressions. If the default number of replicas is 5, the extra replica is placed on the last node, that is, the node labeled with label-3.

When the ACLs function is enabled and the user does not have the permission to access the labels used in the expression, the DataNode with the label is not selected for the replica.

Deletion of Redundant Block Replicas
------------------------------------

If the number of block replicas exceeds the value of **dfs.replication** (number of file replicas specified by the user), HDFS will delete redundant block replicas to ensure cluster resource usage.

The deletion rules are as follows:

-  Preferentially delete replicas that do not meet any expression.

   For example: The default number of file replicas is **3**.

   The label expression of **/test** is **LA[replica=1],LB[replica=1],LC[replica=1]**.

   The file replicas of **/test** are distributed on four nodes (D1 to D4), corresponding to labels (LA to LD).

   .. code-block::

      D1:LA
      D2:LB
      D3:LC
      D4:LD

   Then, block replicas on node D4 will be deleted.

-  If all replicas meet the expressions, delete the redundant replicas which are beyond the number specified by the expression.

   For example: The default number of file replicas is **3**.

   The label expression of **/test** is **LA[replica=1],LB[replica=1],LC[replica=1]**.

   The file replicas of **/test** are distributed on the following four nodes, corresponding to the following labels.

   .. code-block::

      D1:LA
      D2:LA
      D3:LB
      D4:LC

   Then, block replicas on node D1 or D2 will be deleted.

-  If a file owner or group of a file owner cannot access a label, preferentially delete the replica from the DataNode mapped to the label.

Example of label-based block placement policy
---------------------------------------------

Assume that there are six DataNodes, namely, dn-1, dn-2, dn-3, dn-4, dn-5, and dn-6 in a cluster and the corresponding IP address range is 10.1.120.[1-6]. Six directories must be configured with label expressions. The default number of block replicas is **3**.

-  The following provides three expressions of the DataNode label in **host2labels** file. The three expressions have the same function.

   -  Regular expression of the host name

      .. code-block::

         /dn-[1456]/ = label-1,label-2
         /dn-[26]/ = label-1,label-3
         /dn-[3456]/ = label-1,label-4
         /dn-5/ = label-5

   -  IP address range expression

      .. code-block::

         10.1.120.[1-6] = label-1
         10.1.120.1 = label-2
         10.1.120.2 = label-3
         10.1.120.[3-6] = label-4
         10.1.120.[4-6] = label-2
         10.1.120.5 = label-5
         10.1.120.6 = label-3

   -  Common host name expression

      .. code-block::

         /dn-1/ = label-1, label-2
         /dn-2/ = label-1, label-3
         /dn-3/ = label-1, label-4
         /dn-4/ = label-1, label-2, label-4
         /dn-5/ = label-1, label-2, label-4, label-5
         /dn-6/ = label-1, label-2, label-3, label-4

-  The label expressions of the directories are set as follows:

   .. code-block::

      /dir1 = label-1
      /dir2 = label-1 && label-3
      /dir3 = label-2 || label-4[replica=2]
      /dir4 = (label-2 || label-3) && label-4
      /dir5 = !label-1
      /sdir2.txt = label-1 && label-3[replica=3,fallback=NONE]
      /dir6 = label-4[replica=2],label-2

   .. note::

      For details about the label expression configuration, see the **hdfs nodelabel -setLabelExpression** command.

   The file data block storage locations are as follows:

   -  Data blocks of files in the **/dir1** directory can be stored on any of the following nodes: dn-1, dn-2, dn-3, dn-4, dn-5, and dn-6.
   -  Data blocks of files in the **/dir2** directory can be stored on the dn-2 and dn-6 nodes. The default number of block replicas is **3**. The expression matches only two DataNodes. The third replica will be stored on one of the remaining nodes in the cluster.
   -  Data blocks of files in the **/dir3** directory can be stored on any three of the following nodes: dn-1, dn-3, dn-4, dn-5, and dn-6.
   -  Data blocks of files in the **/dir4** directory can be stored on the dn-4, dn-5, and dn-6 nodes.
   -  Data blocks of files in the **/dir5** directory do not match any DataNode and will be stored on any three nodes in the cluster, which is the same as the default block selection policy.
   -  For the data blocks of the **/sdir2.txt** file, two replicas are stored on the dn-2 and dn-6 nodes. The left one is not stored in the node because **fallback=NONE** is enabled.
   -  Data blocks of the files in the **/dir6** directory are stored on the two nodes with label-4 selected from dn-3, dn-4, dn-5, and dn-6 and another node with label-2. If the specified number of file replicas in the **/dir6** directory is more than 3, the extra replicas will be stored on a node with label-2.

Restrictions
------------

In configuration files, **key** and **value** are separated by equation signs (=), colons (:), and whitespace. Therefore, the host name of the **key** cannot contain these characters because these characters may be considered as separators.
