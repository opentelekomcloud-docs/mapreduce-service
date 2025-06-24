:original_name: admin_guide_000222.html

.. _admin_guide_000222:

Restoring NameNode Data
=======================

Scenario
--------

NameNode data needs to be recovered in the following scenarios: data is modified or deleted unexpectedly and needs to be restored. After an administrator performs critical data adjustment in NameNode, an exception occurs or the operation has not achieved the expected result. All modules are faulty and become unavailable. Data is migrated to a new cluster.

System administrators can create a recovery task in MRS Manager to recover NameNode data. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.

   -  To recover data when the service is running properly, you are advised to manually back up the latest management data before recovering data. Otherwise, the NameNode data that is generated after the data backup and before the data recovery will be lost.

   -  It is recommended that a data restoration task restore the metadata of only one component to prevent the data restoration of other components from being affected by stopping a service or instance. If data of multiple components is restored at the same time, data restoration may fail.

      HBase metadata cannot be restored at the same time as NameNode metadata. As a result, data restoration fails.

Impact on the System
--------------------

-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is recovered, the NameNode needs to be restarted and is unavailable during the restart.
-  After data is restored, metadata and service data may not be matched, the HDFS enters the security mode, and the HDFS service fails to be started.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  You have logged in to MRS Manager. For details, see :ref:`Logging In to MRS Manager <admin_guide_000004>`.
-  On MRS Manager, all the NameNode role instances whose data is to be recovered are stopped. Other HDFS role instances must keep running. After data is recovered, the NameNode role instances need to be restarted. The NameNode role instances cannot be accessed during the restart.
-  The NameNode backup files are stored **Data path/LocalBackup/** on the active management node.

Procedure
---------

#. On MRS Manager, click **Cluster**, click the name of the desired cluster, and choose **Services** > **HDFS**. On the displayed page, click **Instance** and click **NameNode** to check whether the NameNode instances of the data to be restored are stopped. If the NameNode instances are not stopped, stop them.

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. In the **Operation** column of a specified task in the task list, choose **More** > **View History** to view historical backup task execution records.

   In the displayed window, locate a specified success record and click **View** in the **Backup Path** column to view the backup path information of the task and find the following information:

   -  **Backup Object** specifies the data source of the backup data.

   -  **Backup Path** specifies the full path where the backup files are saved.

      Select the correct item, and manually copy the full path of backup files in **Backup Path**.

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Restoration Management**.

#. Click **Create**.

#. Set **Task Name** to the name of the restoration task.

#. Select the cluster to be operated from **Recovery Object**.

#. In the **Restoration Configuration** area, select **NameNode**.

#. Set **Path Type** of **NameNode** to a backup directory type.

   The settings vary according to backup directory types:

   -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node.

      If you select **LocalDir**, set the following parameters:

      -  **Source Path**: indicates the full path of the backup file on the local disk, for example, *Backup path/Backup task name_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

      If you select **RemoteHDFS**, set the following parameters:

      -  **Source NameService Name**: indicates the NameService name of the backup data cluster. You can enter the built-in NameService name of the remote cluster, for example, **haclusterX**, **haclusterX1**, **haclusterX2**, **haclusterX3**, or **haclusterX4**. You can also enter a configured NameService name of the remote cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Source NameNode IP Address**: indicates the NameNode service plane IP address of the standby cluster, supporting the active node or standby node.
      -  **Source Path**: indicates the full path of HDFS directory for storing backup data of the standby cluster, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **NFS**: indicates that backup files are stored in the NAS using the NFS protocol. If you select **NFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **CIFS**: indicates that backup files are stored in the NAS using the CIFS protocol. If you select **CIFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **SFTP**: indicates that backup files are stored in the server using the SFTP protocol.

      If you select **SFTP**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.

      -  **Server IP Address**: indicates the IP address of the server where the backup data is stored.
      -  **Port**: indicates the port number used to connect to the backup server over the SFTP protocol. The default value is **22**.
      -  **Username**: indicates the username for connecting to the server using the SFTP protocol.
      -  **Password**: indicates the password for connecting to the server using the SFTP protocol.
      -  **Source Path**: indicates the full path of the backup file on the backup server, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **OBS**: indicates that backup files are stored in OBS.

      If you select **OBS**, set the following parameters:

      -  **Source Path**: indicates the full OBS path of a backup file, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

         .. note::

            Only MRS 3.1.0 or later supports saving backup files in OBS.

#. Click **OK**.

#. In the restoration task list, locate a created task and click **Start** in the **Operation** column to execute the restoration task.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.

#. On MRS Manager, click **Cluster**, click the name of the desired cluster, and choose **Services** > **HDFS**. On the displayed page, click **Configurations** and click **All Configurations**.

   On the displayed page, enter the password of the administrator who has logged in for authentication and click **OK**. After the system displays "Operation succeeded", click **Finish**. The service is started successfully.
