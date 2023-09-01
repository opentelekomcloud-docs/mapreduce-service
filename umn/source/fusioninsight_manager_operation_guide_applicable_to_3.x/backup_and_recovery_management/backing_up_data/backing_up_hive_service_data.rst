:original_name: admin_guide_000210.html

.. _admin_guide_000210:

Backing Up Hive Service Data
============================

Scenario
--------

To ensure Hive service data security routinely or before a major operation on Hive (such as upgrade or migration), you need to back up Hive service data. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on FusionInsight Manager to back up Hive service data. Both automatic and manual backup tasks are supported.

-  Hive backup and restoration cannot identify the service and structure relationships of objects such as Hive tables, indexes, and views. When executing backup and restoration tasks, you need to manage unified restoration points based on service scenarios to ensure proper service running.
-  Hive backup and restoration do not support Hive on RDB data tables. You need to back up and restore original data tables in external databases independently.
-  If the backup data of the standby cluster is lost in an existing Hive backup task that contains Hive on HBase tables, the next incremental backup will fail, and you need to create a Hive backup task again. However, the next full backup task will be normal.
-  After the backup function of FusionInsight Manager is used to back up the HDFS directories at the Hive table level, the Hive tables cannot be deleted and recreated.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster.
-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same FusionInsight Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.
-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.

-  Backup policies, including the backup task type, period, backup object, backup directory, and Yarn queue required by the backup task are planned based on service requirements.
-  The HDFS in the standby cluster has sufficient space. You are advised to save backup files in a custom directory.
-  On the HDFS client, you have executed the **hdfs lsSnapshottableDir** command as user **hdfs** to check the list of directories for which HDFS snapshots have been created in the current cluster and ensured that the HDFS parent directory or subdirectory where data files to be backed up are stored does not have HDFS snapshots. Otherwise, the backup task cannot be created.
-  If you want to back up data to NAS, you have deployed the NAS server in advance.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

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
      | Backup Policy                     | -  **Full backup at the first time and incremental backup subsequently**                                                                                                                                                                                                              |
      |                                   | -  **Full backup every time**                                                                                                                                                                                                                                                         |
      |                                   | -  **Full backup once every n times**                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                       |
      |                                   | .. note::                                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                       |
      |                                   |    -  Incremental backup is not supported when Manager data and component metadata are backed up. Only **Full backup every time** is supported.                                                                                                                                       |
      |                                   |    -  If **Path Type** is set to **NFS** or **CIFS**, incremental backup cannot be used. When incremental backup is used for NFS or CIFS backup, the latest full backup data is updated each time the incremental backup is performed. Therefore, no new recovery point is generated. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. In **Configuration**, choose **Hive** > **Hive**.

#. Set **Path Type** of **Hive** to a backup directory type.

   The following backup directory types are supported:

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster. If you select this option, set the following parameters:

      -  **Destination NameService Name**: indicates the NameService name of the standby cluster. You can set it to the NameService name (**haclusterX**, **haclusterX1**, **haclusterX2**, **haclusterX3**, or **haclusterX4**) of the built-in remote cluster of the cluster, or the NameService name of a configured remote cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Target NameNode IP Address**: indicates the IP address of the NameNode service plane in the standby cluster. It can be of an active or standby node.
      -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **NFS**: indicates that backup files are stored in the NAS using the NFS protocol. If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

   -  **CIFS**: indicates that backup files are stored in the NAS using the CIFS protocol. If you select this option, set the following parameters:

      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Server IP Address**: indicates the IP address of the NAS server.
      -  **Port**: indicates the port number used to connect to the NAS server over the CIFS protocol. The default value is **445**.
      -  **Username**: indicates the username set when the CIFS protocol is configured.
      -  **Password**: indicates the password set when the CIFS protocol is configured.
      -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
      -  **Server Shared Path**: indicates the configured shared directory of the NAS server. (The shared path of the server cannot be set to the root directory, and the user group and owner group of the shared path must be **nobody:nobody**.)
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.
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
      -  **Queue Name**: indicates the name of the Yarn queue used for backup task execution. The name must be the same as the name of the queue that is running properly in the cluster.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.
      -  **NameService Name**: indicates the NameService name of the backup directory. The default value is **hacluster**.

#. Set **Maximum Number of Recovery Points** to the number of snapshots that can be retained in the cluster.

#. Set **Backup Content** to one or multiple Hive tables to be backed up.

   You can select backup data using either of the following methods:

   -  Adding a backup data file

      Click the name of a database in the navigation tree to show all the tables in the database, and select specified tables.

   -  Selecting using regular expressions

      a. Click **Query Regular Expression**.
      b. Enter the database where the Hive tables are located in the first text box as prompted. The database must be the same as the existing database, for example, **default**.
      c. Enter a regular expression in the second text box. Standard regular expressions are supported. For example, to get all tables in the database, enter **([\\s\\S]*?)**. To get tables whose names consist of letters and digits, for example, **tb1**, enter **tb\\d\***.
      d. Click **Refresh** to view the displayed tables in **Directory Name**.
      e. Click **Synchronize** to save the result.

      .. note::

         -  When entering regular expressions, click |image1| or |image2| to add or delete an expression.
         -  If the selected table or directory is incorrect, click **Clear Selected Node** to deselect it.

#. Click **Verify** to check whether the backup task is configured correctly.

   The possible causes of the verification failure are as follows:

   -  The target NameNode IP address is incorrect.
   -  The queue name is incorrect.
   -  The parent directory or subdirectory of the HDFS directory where data files to be backed up are stored has HDFS snapshots.
   -  The directory or table to be backed up does not exist.
   -  The name of the NameService is incorrect.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name_Data source_Task creation time*, and the subdirectory is used to save latest data source backup files. All the backup file sets are stored in the related snapshot directories.

.. |image1| image:: /_static/images/en-us_image_0000001442494045.png
.. |image2| image:: /_static/images/en-us_image_0000001442413869.png
