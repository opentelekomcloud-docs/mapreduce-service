:original_name: mrs_01_0553.html

.. _mrs_01_0553:

Backing Up Metadata
===================

Scenario
--------

To ensure the security of metadata either on a routine basis or before and after performing critical metadata operations (such as scale-out, scale-in, patch installation, upgrades, and migration), metadata must be backed up. The backup data can be used to recover the system if an exception occurs or if the operation has not achieved the expected result. This minimizes the adverse impact on services. Metadata includes data of OMS, LdapServer, DBService, and NameNode. MRS Manager data to be backed up includes OMS data and LdapServer data.

By default, metadata backup is supported by the **default** task. This section describes how to create a backup task and back up metadata on MRS Manager. Both automatic backup tasks and manual backup tasks are supported.

Prerequisites
-------------

-  A standby cluster for backing up data has been created, and the network is connected. The inbound rules of the two security groups on the peer cluster have been added to the two security groups in each cluster to allow all access requests of all protocols and ports of all ECSs in the security groups.
-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.

Procedure
---------

#. Create a backup task.

   a. On MRS Manager, choose **System** > **Back Up Data**.
   b. Click **Create Backup Task**.

#. Configure a backup policy.

   a. Set **Task Name** to the name of the backup task.

   b. Set **Backup Mode** to the type of the backup task. **Periodic** indicates that the backup task is periodically executed. **Manual** indicates that the backup task is manually executed.

      To create a periodic backup task, set the following parameters:

      -  **Started**: indicates the time when the task is started for the first time.
      -  **Period**: indicates the task execution interval. The options include **By hour** and **By day**.
      -  **Backup Policy**: indicates the volume of data to be backed up in each task execution. The options include **Full backup at the first time and incremental backup later**, **Full backup every time**, and **Full backup once every n times**. If you select **Full backup once every n times**, you need to specify the value of **n**.

#. Select backup sources.

   In the **Configuration** area, select **OMS** and **LdapServer** under **Metadata**.

#. Set backup parameters.

   a. Set **Path Type** of **OMS** and **LdapServer** to a backup directory type.

      The following backup directory types are supported:

      -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node and the standby management node automatically synchronizes the backup files. By default, the backup files are stored in *Data storage path*\ **/LocalBackup/**. If you select **LocalDir**, you need to set the maximum number of copies to specify the number of backup files that can be retained in the backup directory.
      -  **LocalHDFS**: indicates that the backup files are stored in the HDFS directory of the current cluster. If you select **SFTP**, set the following parameters:

         -  **Target Path**: indicates the HDFS directory for storing the backup files. The save path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory.
         -  **Max Number of Backup Copies**: indicates the number of backup files that can be retained in the backup directory.
         -  **Target Instance Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   b. Click **OK**.

#. Execute the backup task.

   In the **Operation** column of the created task in the backup task list, click **Back Up Now** if **Backup Mode** is set to **Periodic** or click **Start** If **Backup Mode** is set to **Manual** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files. The format of the backup file name is *Version_Data source_Task execution time*\ **.tar.gz**.
