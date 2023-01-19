:original_name: mrs_01_0510.html

.. _mrs_01_0510:

Using the ReplicationSyncUp Tool
================================

Prerequisites
-------------

#. Active and standby clusters have been installed and started.
#. Time is consistent between the active and standby clusters and the NTP service on the active and standby clusters uses the same time source.
#. When the HBase service of the active cluster is stopped, the ZooKeeper and HDFS services must be started and run.
#. ReplicationSyncUp must be run by the system user who starts the HBase process.
#. In security mode, ensure that the HBase system user of the standby cluster has the read permission on HDFS of the active cluster. This is because that it will update the ZooKeeper nodes and HDFS files of the HBase system.
#. When HBase of the active cluster is faulty, the ZooKeeper, file system, and network of the active cluster are still available.

Scenarios
---------

The replication mechanism can use WAL to synchronize the state of a cluster with the state of another cluster. After HBase replication is enabled, if the active cluster is faulty, ReplicationSyncUp synchronizes incremental data from the active cluster to the standby cluster using the information from the ZooKeeper node. After data synchronization is complete, the standby cluster can be used as an active cluster.

Parameter Configuration
-----------------------

+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| Parameter                          | Description                                                                                                                                                                                             | Default Value |
+====================================+=========================================================================================================================================================================================================+===============+
| hbase.replication.bulkload.enabled | Whether to enable the bulkload data replication function. The parameter value type is Boolean. To enable the bulkload data replication function, set this parameter to **true** for the active cluster. | **false**     |
+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| hbase.replication.cluster.id       | ID of the source HBase cluster. After the bulkload data replication is enabled, this parameter is mandatory and must be defined in the source cluster. The parameter value type is String.              | ``-``         |
+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

Tool Usage
----------

Run the following command on the client of the active cluster:

**hbase org.apache.hadoop.hbase.replication.regionserver.ReplicationSyncUp -Dreplication.sleep.before.failover=1**

.. note::

   **replication.sleep.before.failover** indicates sleep time required for replication of the remaining data when RegionServer fails to start. You are advised to set this parameter to 1 second to quickly trigger replication.

Precautions
-----------

#. When the active cluster is stopped, this tool obtains the WAL processing progress and WAL processing queue from the ZooKeeper Node (RS znode) and copies the queues that are not copied to the standby cluster.
#. RegionServer of each active cluster has its own znode under the replication node of ZooKeeper in the standby cluster. It contains one znode of each peer cluster.
#. If RegionServer is faulty, each RegionServer in the active cluster receives a notification through the watcher and attempts to lock the znode of the faulty RegionServer, including its queues. The successfully created RegionServer transfers all queues to the znode of its own queue. After queues are transferred, they are deleted from the old location.
#. When the active cluster is stopped, ReplicationSyncUp synchronizes data between active and standby clusters using the information from the ZooKeeper node. In addition, WALs of the RegionServer znode will be moved to the standby cluster.

Restrictions and Limitations
----------------------------

If the standby cluster is stopped or the peer relationship is closed, the tool runs normally but the peer relationship cannot be replicated.
