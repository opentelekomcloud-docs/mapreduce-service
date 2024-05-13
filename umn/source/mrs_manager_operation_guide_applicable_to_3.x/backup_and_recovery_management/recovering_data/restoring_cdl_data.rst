:original_name: admin_guide_000345.html

.. _admin_guide_000345:

Restoring CDL Data
==================

Scenario
--------

CDL data needs to be restored in the following scenarios: Data is modified or deleted unexpectedly and needs to be restored. After an administrator performs major operations (such as upgrade and data adjustment) on CDL, an exception occurs or the expected result is not achieved. All modules are faulty and become unavailable. Data is migrated to a new cluster.

CDL metadata is stored in DBService and Kafka. A system administrator can create DBService and Kafka restoration tasks on MRS Manager to restore CDL data. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To restore the data when services are normal, manually back up the latest management data first and then restore the data. Otherwise, the DBService and Kafka data that is generated after the data backup and before the data restoration will be lost.
   -  By default, MRS clusters use DBService to store metadata of Hive, Hue, Loader, Spark, CDL, and Oozie. Restoring DBService data will restore the metadata of all these components.

Impact on the System
--------------------

-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is restored, the configurations of the components that depend on DBService may expire and these components need to be restarted.
-  After the metadata is restored, the offset information stored on ZooKeeper by Kafka consumers is rolled back, resulting in repeated consumption.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust must be configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.
-  Cross-cluster replication has been configured for the active and standby clusters. For details, see :ref:`Enabling Cross-Cluster Replication <admin_guide_000200>`.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.

-  The status of the active and standby DBService instances is normal. If the status is abnormal, data restoration cannot be performed.

-  The Kafka service is disabled first, and then enabled upon data restoration.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. In the row where the specified backup task is located, choose **More** > **View History** in the **Operation** column to display the historical execution records of the backup task.

   In the window that is displayed, select a success record and click **View** in the **Backup Path** column to view its backup path information and find the following information:

   -  **Backup Object**: indicates the backup data source.

   -  **Backup Path**: indicates the full path where backup files are stored.

      Select the correct path, and manually copy the full path of backup files in **Backup Path**.

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Restoration Management**.

#. Click **Create**.

#. Set **Task Name** to the name of the restoration task.

#. Select the cluster to be operated from **Recovery Object**.

#. In the **Restoration Configuration** area, select **DBService** and **Kafka**.

   .. note::

      If multiple DBService or Kafka services are installed, select the DBService or Kafka services to be restored.

#. Set **Path Type** of **DBService** to a backup directory type. For details about how to configure the parameters, see :ref:`8 <admin_guide_000359__li4457996415256>`.

#. Set **Path Type** of **Kafka** to a backup directory type. For details about how to configure the parameters, see :ref:`8 <admin_guide_000361__li4457996415256>`.

#. Click **OK**.

#. In the restoration task list, locate the row where the created task is located, and click **Start** in the **Operation** column.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.
