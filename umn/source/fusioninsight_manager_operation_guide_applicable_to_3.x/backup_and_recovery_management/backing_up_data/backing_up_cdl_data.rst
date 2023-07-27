:original_name: admin_guide_000343.html

.. _admin_guide_000343:

Backing Up CDL Data
===================

Scenario
--------

To ensure CDL service data security routinely or before a major operation on CDL (such as upgrade or migration), you need to back up CDL data. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

CDL data is stored in DBService and Kafka. You can create DBService and Kafka backup tasks on FusionInsight Manager to back up CDL data. Both automatic and manual backup tasks are supported.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster.
-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same FusionInsight Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.
-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The backup type, period, policy, and other specifications have been planned based on the service requirements and you have checked whether *Data storage path*\ **/LocalBackup/** has sufficient space on the active and standby management nodes.
-  If you want to back up data to NAS, you have deployed the NAS server in advance.
-  If you want to back up data to OBS, you have connected the current cluster to OBS and have the permission to access OBS.

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

#. Set **Configuration** to **DBService** and **Kafka**.

   .. note::

      If there are multiple DBService or Kafka services, all DBService or Kafka services are backed up by default. You can click **Assign Service** to specify the services to be backed up.

#. Set **Path Type** of **DBService** to a backup directory type. For details about how to set the parameters, see :ref:`7 <admin_guide_000349__li4457996415256>`.

#. Set **Path Type** of **Kafka** to a backup directory type. For details about how to set the parameters, see :ref:`7 <admin_guide_000203__li4457996415256>`.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name*\ **\_**\ *Task creation time*, and the subdirectory is used to save data source backup files.

   The format of the backup file name is *Version*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
