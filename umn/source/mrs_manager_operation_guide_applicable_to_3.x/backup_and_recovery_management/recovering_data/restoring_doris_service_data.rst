:original_name: admin_guide_000424.html

.. _admin_guide_000424:

Restoring Doris Service Data
============================

Scenario
--------

Doris data needs to be recovered in the following scenarios: data is modified or deleted unexpectedly and needs to be restored. After an administrator performs critical data adjustment in the Doris, an exception occurs or the operation has not achieved the expected result. All modules are faulty and become unavailable. Data is migrated to a new cluster.

System administrators can create a recovery task in MRS Manager to recover Doris data. Only manual restoration tasks are supported.

When executing backup and restoration tasks, you need to manage unified restoration points based on service scenarios to ensure proper service running.

.. important::

   -  This topic is available for clusters of MRS 3.5.0 and later only.
   -  Data can be restored only when the system version during data backup is the same as the current system version.
   -  To restore data when services are normal, manually back up the latest management data before restoring data. Otherwise, the Doris data generated after data backup and before data restoration will be lost.

Impact on the System
--------------------

After data is restored, the data generated after data backup and before data restoration is lost.

Prerequisites
-------------

-  To restore data from a remote HDFS, the following conditions must be met:

   -  A standby cluster for restoring data has been created, and data in this cluster has been backed up. For details, see :ref:`Backing Up Doris Data <admin_guide_000423>`. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, you do not need to configure mutual trust.
   -  At least one DBroker instance of the Doris service has been deployed in the active cluster.
   -  The time on the active and standby clusters must be the same, and the NTP service on the active and standby clusters uses the same time source.
   -  The value of **hadoop.rpc.protection** of Doris must be the same as that of **hadoop.rpc.protection** of HDFS in both active and standby clusters.

-  If you want to restore data from OBS, you have connected the Doris cluster to OBS and have the permission to access OBS.
-  The database for storing restored data tables, the location for storing the data tables in HDFS, and the list of users who can access the restored data have been planned.
-  Check the path for storing Doris backup files.
-  Stop the upper-layer Doris applications.


Restoring Doris Service Data
----------------------------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. .. _admin_guide_000424__en-us_topic_0000001866255229_li6526329016521:

   In the **Operation** column of a specified task in the task list, click **More** and select **View History** to view historical execution records of backup tasks.

   In the window that is displayed, select a success record and click **View** in the **Backup Path** column to view its backup path information and find the following information:

   -  **Backup Object**: indicates the backup data source.

   -  **Backup Path**: indicates the full path for storing backup files.

      Select the correct path and copy the full path of backup files in **Backup Path**.

#. Choose **Restoration Management** and click **Create**.

#. Set **Task Name** to the name of the restoration task.

#. Select the desired cluster from **Recovery Object**.

#. In **Restoration Configuration**, select **Doris** under **Service data**.

#. Set **Path Type** of **Doris** to a restoration directory type.

   .. table:: **Table 1** Path for data restoration

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Directory Type                    | Description                                                                                                                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================================================================================================================+
      | RemoteHDFS                        | The backup files are stored in the HDFS directory of the standby cluster. If you select this option, you also need to configure the following parameters:                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                                          |
      |                                   | -  **Source NameService Name**: indicates the NameService name of the backup data cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.                                                                                                        |
      |                                   | -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects an IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.                                                                                                                                   |
      |                                   | -  **Source NameNode IP Address**: indicates the service plane IP address of the NameNode in the standby cluster.                                                                                                                                                                                                        |
      |                                   | -  **Source NameNode RPC Port**: indicates the value of **dfs.namenode.rpc.port** in the HDFS configuration of the standby cluster.                                                                                                                                                                                      |
      |                                   | -  **DBroker IP**: indicates the IP address of a service plane where the DBroker role in the cluster is deployed. The DBroker is used to transmit data during restoration.                                                                                                                                               |
      |                                   | -  **Source Path**: indicates the full path of the HDFS directory for storing backup data of the standby cluster. For details, see **Backup Path** obtained in :ref:`2 <admin_guide_000424__en-us_topic_0000001866255229_li6526329016521>`. for example, *Backup path/Backup task name_Data source_Task creation time/*. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | OBS                               | Data is restored from OBS. If you select this option, you also need to configure the following parameters:                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                          |
      |                                   | **Source Path**: indicates the full OBS directory of the backup files. Specify this path by referring to :ref:`2 <admin_guide_000424__en-us_topic_0000001866255229_li6526329016521>`, for example, *Backup path/Backup task name_Data source_Task creation time/*.                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Refresh** and select a Doris backup file set that has been backed up.

#. In the **Data Configuration** area, select one or more pieces of backup data for **Select Data** based on service requirements.

   Configuration restrictions are as follows:

   -  There is a database with the same name as the original database of the selected backup data in the Doris of the cluster.
   -  The backup data is restored to the backup table with the same name as the original table in the database.
   -  If there is a table with the same name in Doris, ensure that the structures of the two tables are the same, including table names, columns, partitions, and materialized views.

#. Set **Original Configurations** to **true**, indicating that the configuration of the backup data, such as the number of copies, will be used. If this parameter is set to **false**, the default configuration is used to create a table.

#. Click **OK**.

#. In the restoration task list, locate a created task and click **Start** in the **Operation** column to execute the restoration task.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be re-executed.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to re-execute the task.
