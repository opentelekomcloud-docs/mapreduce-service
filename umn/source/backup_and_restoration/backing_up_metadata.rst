:original_name: mrs_01_0319.html

.. _mrs_01_0319:

Backing Up Metadata
===================

Scenario
--------

To ensure metadata security or before and after a critical operation (such as scale-out/scale-in, patch installation, upgrade, or migration) on the metadata, you need to back up the metadata. The backup data can be used to recover the system in time if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impact on services. Metadata includes data of OMS, LdapServer, DBService, and NameNode. MRS Manager data to be backed up includes OMS data and LdapServer data.

By default, metadata backup is supported by the **default** task. This section describes how to create a backup task and back up metadata on MRS. You can back up data both automatically or manually.

Prerequisites
-------------

-  A standby cluster for backing up data has been created, and the network is normal. For the security group of each cluster, you need to add inbound rules of the security group of the peer cluster to allow access requests from all ECSs in the security group using all protocols and ports.
-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. Create a backup task.

   a. On the cluster details page, click **Backups & Restorations**.
   b. On the **Backups** tab page, click **Create Backup Task**.

#. Configure a backup policy.

   a. Set **Task Name** to the name of the backup task.

   b. Set **Backup Mode** to the type of the backup task. **Periodic** indicates that the backup task is periodically executed and **Manual** indicates that the backup task is manually executed.

      To create a periodic backup task, set the following parameters:

      -  **Started**: indicates the time when the task is started for the first time.
      -  **Period**: indicates the task execution interval. The options include **By hour** and **By day**.
      -  **Backup Policy**: indicates the volume of data to be backed up in each task execution. Supports **Full backup at the first time and incremental backup later**, **Full backup every time**, and **Full backup once every n times**. If you select **Full backup once every n times**, you need to specify the value of **n**.

#. Select backup sources.

   In the **Configuration** area, select the metadata type, such as **OMS** and **LdapServer**.

#. Set backup parameters.

   a. Set **Path Type** of **OMS** and **LdapServer** to the backup directory type.

      The following backup directory types are supported:

      -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node and the standby management node automatically synchronizes the backup files. By default, the backup files are stored in *Data storage path*\ **/LocalBackup/**. If you select **LocalDir**, you need to set the maximum number of copies to specify the number of backup files that can be retained in the backup directory.
      -  **LocalHDFS**: indicates that the backup files are stored in the HDFS directory of the current cluster. If you select **LocalHDFS**, set the following parameters:

         -  **Target Path**: indicates the HDFS directory for storing the backup files. The save path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory.
         -  **Max Number of Backup Copies**: indicates the number of backup files that can be retained in the backup directory.
         -  **Target Instance Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   b. Click **OK**.

#. Execute a backup task. In the **Operation** column of the created task in the backup task list, perform the following operations:

   -  If **Backup Type** is set to **Periodic**, click **Back Up Now**.
   -  If **Backup Type** is set to **Manual**, click **Start** to start the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files. The format of the backup file name is *Version_Data source_Task execution time*\ **.tar.gz**.
