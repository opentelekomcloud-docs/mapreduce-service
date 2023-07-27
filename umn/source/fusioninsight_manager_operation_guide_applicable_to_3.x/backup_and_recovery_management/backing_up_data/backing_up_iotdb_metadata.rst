:original_name: admin_guide_000350.html

.. _admin_guide_000350:

Backing Up IoTDB Metadata
=========================

Scenario
--------

To ensure IoTDB metadata security and prevent the IoTDB service from being unavailable due to IoTDB metadata file damages, you need to back up IoTDB metadata. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on FusionInsight Manager to back up IoTDB metadata. Both automatic and manual backup tasks are supported.

Prerequisites
-------------

-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.

-  If you want to back up data to NAS, you have deployed the NAS server in advance.

-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.

-  Backup policies, including the backup task type, period, backup object, backup directory, and Yarn queue required by the backup task are planned based on service requirements.
-  The HDFS in the standby cluster has sufficient space. You are advised to save backup files in a custom directory.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the cluster to be operated from **Backup Object**.

#. Set **Mode** to the type of the backup task.

   **Periodic** indicates that the backup task is executed by the system periodically. **Manual** indicates that the backup task is executed manually.

   .. table:: **Table 1** Periodic backup parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                |
      +===================================+============================================================================================================================+
      | Started                           | Indicates the time when the task is started for the first time.                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
      | Period                            | The task execution interval. Value options include **Hours** and **Days**.                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
      | Backup Policy                     | Indicates a periodic backup policy.                                                                                        |
      |                                   |                                                                                                                            |
      |                                   | -  **Full backup at the first time and incremental backup subsequently**                                                   |
      |                                   | -  **Full backup every time**                                                                                              |
      |                                   | -  **Full backup once every n times**                                                                                      |
      |                                   |                                                                                                                            |
      |                                   | .. note::                                                                                                                  |
      |                                   |                                                                                                                            |
      |                                   |    Incremental backup is not supported when component metadata is backed up. Only **Full backup every time** is supported. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+

#. In **Configuration**, select **IoTDB** under **Metadata and other data**.

   .. note::

      If there are multiple IoTDB services, all IoTDB services are backed up by default. You can click **Assign Service** to specify the services to be backed up.

#. Set **Path Type** of **IoTDB** to a backup directory type.

   The following backup directory types are supported:

   -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node and the standby management node automatically synchronizes the backup files. By default, the backup files are stored in *Data storage path*\ **/LocalBackup/**.

      If you select this option, you need to set the maximum number of replicas to specify the number of backup file sets that can be retained in the backup directory.

   -  **NFS**: indicates that backup files are stored in the NAS using the NFS protocol.

      If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.

      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

      If you select this option, set the following parameters:

      -  **Destination NameService Name**: indicates the NameService name of the standby cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Destination Active NameNode IP Address**: indicates the service plane IP address of the active NameNode in the standby cluster.
      -  **Destination Standby NameNode IP Address**: indicates the service plane IP address of the standby NameNode in the standby cluster.
      -  **Destination NameNode RPC Port**: indicates the value of **dfs.namenode.rpc.port** in the HDFS basic configuration of the standby cluster.
      -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

   -  **CIFS**: indicates that backup files are stored in the NAS using the CIFS protocol.

      If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.

      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

   -  **SFTP**: indicates that backup files are stored in the server using the SFTP protocol.

      If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the server where the backup data is stored.
      -  **Port**: indicates the port number used to connect to the backup server over the SFTP protocol. The default value is **22**.
      -  **Username**: indicates the username for connecting to the server using the SFTP protocol.
      -  **Password**: indicates the password for connecting to the server using the SFTP protocol.
      -  **Server Shared Path**: indicates the backup path on the SFTP server.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files.

   The format of the backup file name is *Version*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
