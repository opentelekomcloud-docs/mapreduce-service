:original_name: admin_guide_000208.html

.. _admin_guide_000208:

Backing Up NameNode Data
========================

Scenario
--------

To ensure NameNode service data security routinely or before a major operation on NameNode (such as upgrade or migration), you need to back up NameNode data. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on MRS Manager to back up NameNode data. Both automatic and manual backup tasks are supported.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster.
-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.
-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.

-  If you want to back up data to NAS, you have deployed the NAS server in advance.
-  If you want to back up data to OBS, you have connected the current cluster to OBS and have the permission to access OBS.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the cluster to be operated from **Backup Object**.

#. Set **Mode** to the type of the backup task.

   **Periodic** indicates that the backup task is executed by the system periodically. **Manual** indicates that the backup task is executed manually.

   .. table:: **Table 1** Periodic backup parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                           |
      +===================================+=======================================================================================================================================================================================================================================================================================+
      | Started                           | Indicates the time when the task is started for the first time.                                                                                                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Period                            | Indicates the task execution interval. The options include **Hours** and **Days**.                                                                                                                                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Backup Policy                     | Only **Full backup every time** is supported.                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                       |
      |                                   | .. note::                                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                       |
      |                                   |    -  Incremental backup is not supported when Manager data and component metadata are backed up. Only **Full backup every time** is supported.                                                                                                                                       |
      |                                   |    -  If **Path Type** is set to **NFS** or **CIFS**, incremental backup cannot be used. When incremental backup is used for NFS or CIFS backup, the latest full backup data is updated each time the incremental backup is performed. Therefore, no new recovery point is generated. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. In **Configuration**, select **NameNode**.

#. Set **Path Type** of **NameNode** to a backup directory type.

   The following backup directory types are supported:

   -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node and the standby management node automatically synchronizes the backup files. By default, the backup files are stored in *Data storage path*\ **/LocalBackup/**.

      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster. If you select this option, set the following parameters:

      -  **Destination NameService Name**: indicates the NameService name of the standby cluster. You can set it to the NameService name (**haclusterX**, **haclusterX1**, **haclusterX2**, **haclusterX3**, or **haclusterX4**) of the built-in remote cluster of the cluster, or the NameService name of a configured remote cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Target NameNode IP Address**: indicates the service plane IP address of the NameNode in the standby cluster.
      -  **Target Path**: indicates the path for storing backup files.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.

   -  **NFS**: indicates that backup files are stored in the NAS using the NFS protocol. If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **CIFS**: indicates that backup files are stored in the NAS using the CIFS protocol. If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **SFTP**: indicates that backup files are stored in the server using the SFTP protocol.

      If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.

      -  **Server IP Address**: indicates the IP address of the server where the backup data is stored.
      -  **Port**: indicates the port number used to connect to the backup server over the SFTP protocol. The default value is **22**.
      -  **Username**: indicates the username for connecting to the server using the SFTP protocol.
      -  **Password**: indicates the password for connecting to the server using the SFTP protocol.
      -  **Server Shared Path**: indicates the backup path on the SFTP server.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **OBS**: indicates that backup files are stored in OBS.

      If you select this option, set the following parameters:

      -  **Target Path**: indicates the OBS directory for storing backup data.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

         .. note::

            Only MRS 3.1.0 or later supports data backup to OBS.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files.

   The format of the backup file name is *Version*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
