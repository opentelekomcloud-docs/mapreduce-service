:original_name: admin_guide_000399.html

.. _admin_guide_000399:

Introduction
============

Overview
--------

FusionInsight Manager provides the backup and restoration of system data and user data by component. The system can back up Manager data, component metadata, and service data.

Data can be backed up to local disks (LocalDir), local HDFS (LocalHDFS), remote HDFS (RemoteHDFS), NAS (NFS/CIFS), Object Storage Service (OBS), and SFTP server (SFTP). For details, see :ref:`Backing Up Data <admin_guide_000201>`.

For a component that supports multiple services, multiple instances of a service can be backed up and restored. The backup and restoration operations are consistent with those of a service instance.

.. note::

   Only MRS 3.1.0 or later supports data backup to OBS.

Backup and restoration tasks are performed in the following scenarios:

-  Routine backup is performed to ensure the data security of the system and components.
-  If the system is faulty, the data backup can be used to recover the system.
-  If the active cluster is completely faulty, a mirrored cluster identical to the active cluster needs to be created. You can use the backup data to restore the active cluster.

.. table:: **Table 1** Manager configuration data to be backed up

   +-----------------------+---------------------------------------------------------------------------------------------------------+-----------------------+
   | Backup Type           | Backup Content                                                                                          | Backup Directory Type |
   +=======================+=========================================================================================================+=======================+
   | OMS                   | Database data (excluding alarm data) and configuration data in the cluster management system by default | -  LocalDir           |
   |                       |                                                                                                         | -  LocalHDFS          |
   |                       |                                                                                                         | -  RemoteHDFS         |
   |                       |                                                                                                         | -  NFS                |
   |                       |                                                                                                         | -  CIFS               |
   |                       |                                                                                                         | -  SFTP               |
   |                       |                                                                                                         | -  OBS                |
   +-----------------------+---------------------------------------------------------------------------------------------------------+-----------------------+

.. table:: **Table 2** Component metadata or other data to be backed up

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Backup Type           | Backup Content                                                                                                                                                                                                      | Backup Directory Type |
   +=======================+=====================================================================================================================================================================================================================+=======================+
   | DBService             | Metadata of the components (including Loader, Hive, Spark, Oozie, and Hue) managed by DBService. For a cluster with multiple services installed, back up the metadata of multiple Hive and Spark service instances. | -  LocalDir           |
   |                       |                                                                                                                                                                                                                     | -  LocalHDFS          |
   |                       |                                                                                                                                                                                                                     | -  RemoteHDFS         |
   |                       |                                                                                                                                                                                                                     | -  NFS                |
   |                       |                                                                                                                                                                                                                     | -  CIFS               |
   |                       |                                                                                                                                                                                                                     | -  SFTP               |
   |                       |                                                                                                                                                                                                                     | -  OBS                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Kafka                 | Kafka metadata.                                                                                                                                                                                                     | -  LocalDir           |
   |                       |                                                                                                                                                                                                                     | -  LocalHDFS          |
   |                       |                                                                                                                                                                                                                     | -  RemoteHDFS         |
   |                       |                                                                                                                                                                                                                     | -  NFS                |
   |                       |                                                                                                                                                                                                                     | -  CIFS               |
   |                       |                                                                                                                                                                                                                     | -  OBS                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | NameNode              | HDFS metadata. After multiple NameServices are added, backup and restoration are supported for all of them and the operations are consistent with those of the default hacluster instance.                          | -  LocalDir           |
   |                       |                                                                                                                                                                                                                     | -  RemoteHDFS         |
   |                       |                                                                                                                                                                                                                     | -  NFS                |
   |                       |                                                                                                                                                                                                                     | -  CIFS               |
   |                       |                                                                                                                                                                                                                     | -  SFTP               |
   |                       |                                                                                                                                                                                                                     | -  OBS                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Yarn                  | Information about the Yarn service resource pool.                                                                                                                                                                   |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | HBase                 | **tableinfo** files and data files of HBase system tables.                                                                                                                                                          |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. table:: **Table 3** Service data of specific components to be backed up

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Backup Type           | Backup Content                                                                                                                                                                                                                                           | Backup Directory Type |
   +=======================+==========================================================================================================================================================================================================================================================+=======================+
   | HBase                 | Table-level user data. For a cluster with multiple services installed, backup and restoration are supported for multiple HBase service instances and the backup and restoration operations are consistent with those of a single HBase service instance. | -  RemoteHDFS         |
   |                       |                                                                                                                                                                                                                                                          | -  NFS                |
   |                       |                                                                                                                                                                                                                                                          | -  CIFS               |
   |                       |                                                                                                                                                                                                                                                          | -  SFTP               |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | HDFS                  | Directories or files of user services.                                                                                                                                                                                                                   |                       |
   |                       |                                                                                                                                                                                                                                                          |                       |
   |                       | .. note::                                                                                                                                                                                                                                                |                       |
   |                       |                                                                                                                                                                                                                                                          |                       |
   |                       |    Encrypted directories cannot be backed up or restored.                                                                                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Hive                  | Table-level user data. For a cluster with multiple services installed, backup and restoration are supported for multiple Hive service instances and the backup and restoration operations are consistent with those of a single Hive service instance.   |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Note that some components do not provide data backup or restoration:

-  Kafka supports replicas and allows multiple replicas to be specified when a topic is created.
-  MapReduce and Yarn data is stored in HDFS. Therefore, they rely on the backup and restoration provided by HDFS.
-  Backup and restoration of service data in ZooKeeper are performed by their own upper-layer components.

Principles
----------

**Task**

Before backup or restoration, you need to create a backup or restoration task and set task parameters, such as the task name, backup data source, and type of the directory for storing backup files. Then you can execute the tasks to back up or restore data. When Manager is used to restore the data of HDFS, HBase, Hive, and NameNode, the cluster cannot be accessed.

Each backup task can back up data of different data sources and generate an independent backup file for each data source. All the backup files generated in a backup task form a backup file set, which can be used in restoration tasks. Backup data can be stored on Linux local disks, local cluster HDFS, and standby cluster HDFS.

Backup tasks support full backup and incremental backup policies. Cloud data backup tasks do not support incremental backup. If the backup directory type is NFS or CIFS, incremental backup is not recommended. When incremental backup is used for NFS or CIFS backup, the latest full backup data is updated each time the incremental backup is performed. Therefore, no new recovery point is generated.

.. note::

   Task execution rules:

   -  If a task is being executed, the task cannot be executed repeatedly and other tasks cannot be started at the same time.
   -  The interval at which a periodic task is automatically executed must be greater than 120s. Otherwise, the task is postponed and will be executed in the next period. Manual tasks can be executed at any interval.
   -  When a periodic task is to be automatically executed, the current time cannot be 120s later than the task start time. Otherwise, the task is postponed and executed in the next period.
   -  When a periodic task is locked, it cannot be automatically executed and needs to be manually unlocked.
   -  Before an OMS, DBService, Kafka, or NameNode backup task starts, ensure that the LocalBackup partition on the active management node has not less than 20 GB of available space. Otherwise, the backup task cannot be started.

When planning backup and restoration tasks, select the data to be backed up or restored strictly based on the service logic, data store structure, and database or table association. By default, the system creates periodic backup tasks **default-oms** and **default-cluster ID** at an interval of one hour. OMS metadata and cluster metadata, such as DBService and NameNode, can be fully backed up to local disks.

**Snapshot**

The system uses the snapshot technology to quickly back up data. Snapshots include HBase and HDFS snapshots.

-  HBase snapshots

   An HBase snapshot is a backup file of HBase tables at a specified time point. This backup file does not replicate service data or affect the RegionServer. The HBase snapshot replicates table metadata, including table descriptor, region info, and HFile reference information. The metadata can be used to restore data before the snapshot creation time.

-  HDFS snapshots

   An HDFS snapshot is a read-only backup of HDFS at a specified time point. The snapshot is used in data backup, misoperation protection, and disaster recovery scenarios.

   The snapshot function can be enabled for any HDFS directory to create the related snapshot file. Before creating a snapshot for a directory, the system automatically enables the snapshot function for the directory. Creating a snapshot does not affect any HDFS operation. A maximum of 65,536 snapshots can be created for each HDFS directory.

   When a snapshot is being created for an HDFS directory, the directory cannot be deleted or modified before the snapshot is created. Snapshots cannot be created for the upper-layer directories or subdirectories of the directory.

**DistCp**

Distributed copy (DistCp) is a tool used to replicate a large amount of data in HDFS in a cluster or between the HDFSs of different clusters. In a backup or restoration task of HBase, HDFS, or Hive, if you back up the data to HDFS of the standby cluster, the system invokes DistCp to perform the operation. Install the MRS software of the same version for the active and standby clusters and install the cluster.

DistCp uses MapReduce to implement data distribution, troubleshooting, restoration, and report. DistCp specifies different Map jobs for various source files and directories in the specified list. Each Map job copies the data in the partition that corresponds to the specified file in the list.

If you use DistCp to replicate data between HDFSs of two clusters, configure the cross-cluster mutual trust (mutual trust does not need to be configured for clusters managed by the same FusionInsight Manager) and cross-cluster replication for both clusters. When backing up the cluster data to HDFS in another cluster, you need to install the Yarn component. Otherwise, the backup fails.

**Local rapid restoration**

After using DistCp to back up the HBase, HDFS, and Hive data of the local cluster to the HDFS of the standby cluster, the HDFS of the local cluster retains the backup data snapshots. You can create local rapid restoration tasks to restore data by using the snapshot files in the HDFS of the local cluster.

**NAS**

Network Attached Storage (NAS) is a dedicated data storage server which includes the storage components and embedded system software. It provides the cross-platform file sharing function. By using NFS (supporting NFSv3 and NFSv4) and CIFS (supporting SMBv2 and SMBv3), you can connect the service plane of MRS to the NAS server to back up data to the NAS or restore data from the NAS.

.. note::

   -  Before data is backed up to the NAS, the system automatically mounts the NAS shared address to a local partition of the backup task execution node. After the backup is complete, the system unmounts the NAS shared partition from the backup task execution node.
   -  To prevent backup and restoration failures, do not access the shared address where the NAS server has been mounted to, for example, **/srv/BigData/LocalBackup/nas**, during data backup and restoration.
   -  When service data is backed up to the NAS, DistCp is used.

Specifications
--------------

.. table:: **Table 4** Specifications of the backup and restoration feature

   ======================================================= =============
   Item                                                    Specification
   ======================================================= =============
   Maximum number of backup or restoration tasks           100
   Number of concurrent tasks in a cluster                 1
   Maximum number of waiting tasks                         199
   Maximum size (GB) of backup files on a Linux local disk 600
   ======================================================= =============

.. note::

   If service data is stored in the ZooKeeper upper-layer components, ensure that the number of znodes in a single backup or restoration task is not too large. Otherwise, the task will fail, and the ZooKeeper service performance will be affected. To check the number of znodes in a single backup or restoration task, perform the following operations:

   -  Ensure that the number of znodes in a single backup or restoration task is smaller than the upper limit of OS file handles. Specifically:

      #. To check the upper limit at the system level, run the **cat /proc/sys/fs/file-max** command.
      #. To check the upper limit at the user level, run the **ulimit -n** command.

   -  If the number of znodes in the parent directory exceeds the upper limit, back up and restore data in its sub-directories in batches. To check the number of znodes using ZooKeeper client scripts, perform the following operations:

      #. On FusionInsight Manager, choose **Cluster**, click the name of the desired cluster, choose **Services** > **ZooKeeper** > **Instance**, and view the management IP address of each ZooKeeper role.

      #. Log in to the node where the client is located and run the following command:

         **zkCli.sh -server** *ip*\ **:**\ *port*, where, *ip* can be any management IP address, and the default port number is 2181.

      #. If the following information is displayed, login to the ZooKeeper server is successful:

         .. code-block::

            WatchedEvent state:SyncConnected type:None path:null
            [zk: ip:port(CONNECIED) 0]

      #. Run the **getusage** command to check the number of znodes in the directory to be backed up.

         For example, **getusage /hbase/region**. In the command output, **Node count=xxxxxx** indicates the number of znodes stored in the **region** directory.

.. table:: **Table 5** Specifications of the default task

   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+
   | Item                            | OMS                                                                               | HBase   | Kafka  | DBService | NameNode                     |
   +=================================+===================================================================================+=========+========+===========+==============================+
   | Backup period                   | 1 hour                                                                            |         |        |           |                              |
   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+
   | Maximum number of backups       | 168 (7-day historical data)                                                       |         |        |           | 24 (one-day historical data) |
   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+
   | Maximum size of a backup file   | 10 MB                                                                             | 10 MB   | 512 MB | 100 MB    | 20 GB                        |
   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+
   | Maximum size of disk space used | 1.64 GB                                                                           | 1.64 GB | 84 GB  | 16.41 GB  | 480 GB                       |
   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+
   | Storage path of backup data     | *Data storage path*\ **/LocalBackup/** of the active and standby management nodes |         |        |           |                              |
   +---------------------------------+-----------------------------------------------------------------------------------+---------+--------+-----------+------------------------------+

.. note::

   -  The backup data of the default backup task must be periodically transferred and saved outside the cluster based on the enterprise O&M requirements.
   -  Administrators can create DistCp backup tasks to save OMS, DBService, and NameNode data to external clusters.
   -  The execution time of a cluster data backup task can be calculated using the following formula: Task execution time = Volume of data to be backed up/Network bandwidth between the cluster and the backup device. In practice, you are advised to multiply the calculated time by 1.5 to get the reference value of the task execution time.
   -  Executing a data backup task affects the maximum I/O performance of the cluster. Therefore, you are advised to execute a backup task during off-peak hours.
