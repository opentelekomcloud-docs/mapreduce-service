:original_name: admin_guide_000358.html

.. _admin_guide_000358:

Restoring ClickHouse Metadata
=============================

Scenario
--------

ClickHouse metadata needs to be restored in the following scenarios: Data is modified or deleted unexpectedly and needs to be restored. After a user performs major operations (such as upgrade and migration) on ZooKeeper, an exception occurs or the expected result is not achieved. The ClickHouse component is faulty and becomes unavailable. Data is migrated to a new cluster.

Users can create a ClickHouse restoration task on FusionInsight Manager. Only manual restoration tasks are supported.

.. important::

   -  This function is supported only by MRS 3.1.0 or later.
   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To restore ClickHouse metadata when the service is running properly, you are advised to manually back up the latest ClickHouse metadata before restoration. Otherwise, the ClickHouse metadata that is generated after the data backup and before the data restoration will be lost.
   -  ClickHouse metadata restoration and service data restoration cannot be performed at the same time. Otherwise, service data restoration fails. You are advised to restore service data after metadata restoration is complete.

Impact on the System
--------------------

-  After the metadata is restored, the data generated after the data backup and before the data restoration is lost.
-  After the metadata is restored, the ClickHouse upper-layer applications need to be started.

Prerequisites
-------------

-  You have checked the path for storing ClickHouse metadata backup files.
-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same FusionInsight Manager, mutual trust must be configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. In the **Operation** column of the specified task in the task list, choose **More** > **View History**.

   In the window that is displayed, select a success record and click **View** in the **Backup Path** column to view its backup path information and find the following information:

   -  **Backup Object**: indicates the backup data source.

   -  **Backup Path**: indicates the full path where backup files are stored.

      Select the correct path, and manually copy the full path of backup files in **Backup Path**.

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Restoration Management**.

#. Click **Create**.

#. Set **Task Name** to the name of the restoration task.

#. Select the cluster to be operated from **Recovery Object**.

#. In **Restoration Configuration**, select **ClickHouse** under **Metadata and other data**.

#. Set **Path Type** of **ClickHouse** to a restoration directory type.

   The configurations vary based on backup directory types:

   -  **LocalDir**: indicates that data is restored from the local disk of the active management node.

      If you select this value, you also need to configure the following parameters:

      -  **Source Path**: backup file to be restored, for example, *Backup task name*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
      -  **Logical Cluster**: Enter the ClickHouse logical cluster whose data has been backed up.

   -  **RemoteHDFS**: indicates that data is restored from the HDFS directory of the standby cluster.

      If you select this value option, you also need to configure the following parameters:

      -  **Source NameService Name**: indicates the NameService name of the backup data cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.
      -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
      -  **Source NameNode IP Address**: indicates the IP address of the NameNode service plane in the standby cluster. It can be of an active or standby node.
      -  **Source Path**: indicates the full path of HDFS directory for storing backup data of the standby cluster, for example, *Backup path/Backup task name_Data source_Task creation time/Data source_Task execution time*\ **.tar.gz**.

#. Click **OK**.

#. In the restoration task list, locate the row where the created task is located, and click **Start** in the **Operation** column. In the displayed dialog box, click **OK** to start the restoration task.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.

#. Choose **Cluster** > **Services** and start the ClickHouse service.
