:original_name: admin_guide_000223.html

.. _admin_guide_000223:

Restoring HDFS Service Data
===========================

Scenario
--------

HDFS data needs to be recovered in the following scenarios: data is modified or deleted unexpectedly and needs to be restored. After an administrator performs critical data adjustment in the HDFS, an exception occurs or the operation has not achieved the expected result. All modules are faulty and become unavailable. Data is migrated to a new cluster.

System administrators can create a recovery task in MRS Manager to recover HDFS data. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To recover data when the service is running properly, you are advised to manually back up the latest management data before recovering data. Otherwise, the HDFS data that is generated after the data backup and before the data recovery will be lost.
   -  The HDFS restoration operation cannot be performed for the directories used by running Yarn tasks, for example, **/tmp/logs**, **/tmp/archived**, and **/tmp/hadoop-yarn/staging**. Otherwise, data restoration using Distcp tasks fails due to file loss.

Impact on the System
--------------------

-  During data restoration, user authentication stops and users cannot create new connections.
-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is recovered, the HDFS upper-layer applications need to be started.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The HDFS backup file save path is correct.
-  The HDFS upper-layer applications are stopped.
-  You have logged in to MRS Manager. For details, see :ref:`Logging In to MRS Manager <admin_guide_000004>`.

Procedure
---------

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

#. In **Restoration Configuration**, select **HDFS** under **Service Data**.

#. Set **Path Type** of **HDFS** to a backup directory type.

   The following backup directory types are supported:

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

      If you select **RemoteHDFS**, set the following parameters:

      -  **Source NameService Name**: indicates the NameService name of the backup data cluster. You can enter the built-in NameService name of the remote cluster, for example, **haclusterX**, **haclusterX1**, **haclusterX2**, **haclusterX3**, or **haclusterX4**. You can also enter a configured NameService name of the remote cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Source NameNode IP Address**: indicates the NameNode service plane IP address of the standby cluster, supporting the active node or standby node.
      -  **Source Path**: indicates the full path of HDFS directory for storing backup data of the standby cluster, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

   -  **NFS**: indicates that backup files are stored in NAS using the NFS protocol. If you select **NFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

   -  **CIFS**: indicates that backup files are stored in NAS using the CIFS protocol. If you select **CIFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

   -  **SFTP**: indicates that backup files are stored in the server using the SFTP protocol.

      If you select **SFTP**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.

      -  **Server IP Address**: indicates the IP address of the server where the backup data is stored.
      -  **Port**: indicates the port number used to connect to the backup server over the SFTP protocol. The default value is **22**.
      -  **Username**: indicates the username for connecting to the server using the SFTP protocol.
      -  **Password**: indicates the password for connecting to the server using the SFTP protocol.
      -  **Source Path**: indicates the full path of the backup file on the backup server, for example, *Backup path/Backup task name_Data source_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Target NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

#. In the **Backup Data** column of the **Data Configuration** page, select one or more pieces of backup data that needs to be restored based on service requirements. In the **Target Path** column, specify the target location after backup data restoration.

   You are advised to set **Target Path** to a new path that is different from the backup path.

#. Click **Verify** to check whether the restoration task is configured correctly.

   -  If the queue name is incorrect, the verification fails.
   -  If the specified directory to be restored does not exist, the verification fails.

#. Click **OK**.

#. In the restoration task list, locate a created task and click **Start** in the **Operation** column to execute the restoration task.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.
