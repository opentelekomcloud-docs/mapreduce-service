:original_name: admin_guide_000219.html

.. _admin_guide_000219:

Restoring HBase Service Data
============================

Scenario
--------

HBase data needs to be recovered in the following scenarios: data is modified or deleted unexpectedly and needs to be restored. After an administrator performs critical data adjustment in HBase, an exception occurs or the operation has not achieved the expected result. All modules are faulty and become unavailable. Data is migrated to a new cluster.

System administrators can create a recovery task in MRS Manager to recover HBase data. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To recover data when the service is running properly, you are advised to manually back up the latest management data before recovering data. Otherwise, the HBase data that is generated after the data backup and before the data recovery will be lost.

Impact on the System
--------------------

-  During the data recovery process, the system disables the HBase table to be recovered and the table cannot be accessed in this moment. The data recovery process takes several minutes, during which the HBase upper-layer applications are unavailable.
-  During data restoration, user authentication stops and users cannot create new connections.
-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is recovered, the HBase upper-layer applications need to be started.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The directory for saving the backup file has been checked.
-  The HBase upper-layer applications have been stopped.
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

#. In **Restoration Configuration**, select **HBase** under **Service Data**.

#. Set **Path Type** of **HBase** to a backup directory type.

   The following backup directory types are supported:

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster. If you select **RemoteHDFS**, set the following parameters:

      -  **Source NameService Name**: indicates the NameService name of the backup data cluster. You can enter the built-in NameService name of the remote cluster, for example, **haclusterX**, **haclusterX1**, **haclusterX2**, **haclusterX3**, or **haclusterX4**. You can also enter a configured NameService name of the remote cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Source NameNode IP Address**: indicates the NameNode service plane IP address of the standby cluster, supporting the active node or standby node.
      -  **Source Path**: indicates the full path of the backup file in the HDFS, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

   -  **NFS**: indicates that backup files are stored in the NAS using the NFS protocol. If you select **NFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

   -  **CIFS**: indicates that backup files are stored in the NAS using the CIFS protocol. If you select **CIFS**, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Source Path**: indicates the full path of the backup file on the NAS server, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution.
      -  **Recovery Point List**: Click **Refresh** and select an HDFS directory that has been backed up in the standby cluster.
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
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

#. Set **Backup Data** column in **Data Configuration** to one or multiple backup data sources to be recovered. In the **Target Namespace** column, specify the target naming space after backup data recovery.

   You are advised to set **Target Namespace** to a location that is different from the backup naming space.

#. Set **Force recovery** to **true**, which indicates to forcibly recover all backup data when a data table with the same name already exists. If the data table contains new data added after backup, the new data will be lost after the data recovery. If you set the parameter to **false**, the restoration task is not executed if a data table with the same name exists.

#. Click **Verify** to check whether the restoration task is configured correctly.

   -  If the queue name is incorrect, the verification fails.
   -  If the specified naming space does not exist, the verification fails.
   -  If the forcibly replacement conditions are not met, the verification fails.

#. Click **OK** to save the settings.

#. In the restoration task list, locate a created task and click **Start** in the **Operation** column to execute the restoration task.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.

#. Check whether HBase data is restored in an environment where HBase is newly installed or reinstalled.

   -  If yes, the administrator needs to set new permission for roles on MRS Manager based on the original service plan.
   -  If no, no further operation is required.
