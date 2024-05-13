:original_name: admin_guide_000359.html

.. _admin_guide_000359:

Restoring ClickHouse Service Data
=================================

Scenario
--------

ClickHouse data needs to be restored in the following scenarios: Data is modified or deleted unexpectedly and needs to be restored. After a user performs major operations (such as upgrade and migration) on ClickHouse, an exception occurs or the expected result is not achieved. All modules are faulty and become unavailable. Data is migrated to a new cluster.

Users can create a ClickHouse restoration task on MRS Manager to restore data. Only manual restoration tasks are supported.

The ClickHouse backup and restoration functions cannot identify the service and structure relationships of objects such as ClickHouse tables, indexes, and views. When executing backup and restoration tasks, you need to manage unified restoration points based on service scenarios to ensure proper service running.

.. important::

   -  This function is supported only by MRS 3.1.0 or later.
   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To restore the data when services are normal, manually back up the latest management data first and then restore the data. Otherwise, the ClickHouse data that is generated after the data backup and before the data restoration will be lost.
   -  ClickHouse metadata restoration and service data restoration cannot be performed at the same time. Otherwise, service data restoration fails. You are advised to restore service data after metadata restoration is complete.

Impact on the System
--------------------

-  During data restoration, user authentication stops and users cannot create new connections.
-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is restored, the ClickHouse upper-layer applications need to be started.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust must be configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The database for storing restored data tables, the HDFS save path of data tables, and the list of users who can access restored data are planned.
-  The ClickHouse backup file save path is correct.
-  The ClickHouse upper-layer applications are stopped.
-  You have logged in to MRS Manager. For details, see :ref:`Logging In to MRS Manager <admin_guide_000004>`.

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

#. In **Restoration Configuration**, select **ClickHouse** under **Service data**.

#. .. _admin_guide_000359__li4457996415256:

   Set **Path Type** of **ClickHouse** to a backup directory type.

   Currently, the backup directory supports only the **RemoteHDFS** type.

   -  **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster. If you select this value option, you also need to configure the following parameters:

      -  **Source NameService Name**: indicates the NameService name of the backup data cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Source NameNode IP Address**: indicates the IP address of the NameNode service plane in the standby cluster. It can be of an active or standby node.
      -  Source Path: indicates the full path of HDFS directory for storing backup data of the standby cluster. For details, see the **Backup Path** obtained in step 2, for example, *Backup path/Backup task name_Data source_Task creation time*.
      -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
      -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

#. Click **OK**.

#. In the restoration task list, locate the row where the created task is located, and click **Start** in the **Operation** column.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.
