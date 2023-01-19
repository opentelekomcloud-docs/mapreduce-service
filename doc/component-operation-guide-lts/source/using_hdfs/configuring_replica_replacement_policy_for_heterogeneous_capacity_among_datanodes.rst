:original_name: mrs_01_0804.html

.. _mrs_01_0804:

Configuring Replica Replacement Policy for Heterogeneous Capacity Among DataNodes
=================================================================================

Scenario
--------

By default, NameNode randomly selects a DataNode to write files. If the disk capacity of some DataNodes in a cluster is inconsistent (the total disk capacity of some nodes is large and of some nodes is small), the nodes with small disk capacity will be fully written. To resolve this problem, change the default disk selection policy for data written to DataNode to the available space block policy. This policy increases the probability of writing data blocks to the node with large available disk space. This ensures that the node usage is balanced when disk capacity of DataNodes is inconsistent.

Impact on the System
--------------------

The disk selection policy is changed to **org.apache.hadoop.hdfs.server.blockmanagement.AvailableSpaceBlockPlacementPolicy**. It is proven that the HDFS file write performance optimizes by 3% after the modification.

.. note::

   **The default replica storage policy of the NameNode is as follows:**

   #. First replica: stored on the node where the client resides.
   #. Second replica: stored on DataNodes of the remote rack.
   #. Third replica: stored on different nodes of the same rack for the node where the client resides.

   If there are more replicas, randomly store them on other DataNodes.

   The replica selection mechanism (**org.apache.hadoop.hdfs.server.blockmanagement.AvailableSpaceBlockPlacementPolicy**) is as follows:

   #. First replica: stored on the DataNode where the client resides (the same as the default storage policy).
   #. Second replica:

      -  When selecting a storage node, select two data nodes that meet the requirements.
      -  Compare the disk usages of the two DataNodes. If the difference is smaller than 5%, store the replicas to the first node.
      -  If the difference exceeds 5%, there is a 60% probability (specified by **dfs.namenode.available-space-block-placement-policy.balanced-space-preference-fraction** and default value is **0.6**) that the replica is written to the node whose disk space usage is low.

   #. As for the storage of the third replica and subsequent replicas, refer to that of the second replica.

Prerequisites
-------------

The total disk capacity deviation of DataNodes in the cluster cannot exceed 100%.

Procedure
---------

#. Go to the **All Configurations** page of HDFS by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. Modify the disk selection policy parameters when HDFS writes data. Search for the **dfs.block.replicator.classname** parameter and change its value to **org.apache.hadoop.hdfs.server.blockmanagement.AvailableSpaceBlockPlacementPolicy**.
#. Save the modified configuration. Restart the expired service or instance for the configuration to take effect.
