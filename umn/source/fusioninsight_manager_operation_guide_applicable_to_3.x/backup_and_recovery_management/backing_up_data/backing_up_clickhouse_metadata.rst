:original_name: admin_guide_000348.html

.. _admin_guide_000348:

Backing Up ClickHouse Metadata
==============================

Scenario
--------

To ensure ClickHouse metadata security or before a major operation on ZooKeeper (such as upgrade or migration), you need to back up ClickHouse metadata. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on FusionInsight Manager to back up ClickHouse metadata. Both automatic and manual backup tasks are supported.

.. important::

   This function is supported only by MRS 3.1.0 or later.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster.

-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.
-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same FusionInsight Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the cluster to be operated from **Backup Object**.

#. Set **Mode** to the type of the backup task. **Periodic** indicates that the backup task is periodically executed. **Manual** indicates that the backup task is manually executed.

   To create a periodic backup task, set the following parameters:

   -  **Started**: indicates the time when the task is started for the first time.
   -  **Period**: indicates the task execution interval. The options include **Hours** and **Days**.
   -  **Backup Policy**: Only **Full backup every time** is supported.

#. In **Configuration**, select **ClickHouse** under **Metadata and other data**.

#. Set **Path Type** of **ClickHouse** to a backup directory type.

   The following backup directory types are supported:

   -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node and the standby management node automatically synchronizes the backup files.

      The default storage directory is *Data storage path*\ **/LocalBackup/**, for example, **/srv/BigData/LocalBackup**.

      If you select this option, you need to set the maximum number of replicas to specify the number of backup file sets that can be retained in the backup directory.

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

      This value option is available only after you configure the environment by referring to :ref:`How Do I Configure the Environment When I Create a ClickHouse Backup Task on FusionInsight Manager and Set the Path Type to RemoteHDFS? <admin_guide_000357>`.

      You also need to configure the following parameters:

      -  **Destination NameService Name**: indicates the NameService name of the standby cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Target NameNode IP Address**: indicates the IP address of the NameNode service plane in the standby cluster. It can be of an active or standby node.
      -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files. The format of the backup file name is *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
