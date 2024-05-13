:original_name: admin_guide_000361.html

.. _admin_guide_000361:

Restoring IoTDB Service Data
============================

Scenario
--------

IoTDB service data needs to be restored in the following scenarios: Data is modified or deleted unexpectedly and needs to be restored. After an administrator performs major operations (such as upgrade and data adjustment) on IoTDB, an exception occurs or the expected result is not achieved. All modules are faulty and become unavailable. Data is migrated to a new cluster.

System administrators can create an IoTDB restoration task on MRS Manager. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To restore the data when services are normal, manually back up the latest management data first and then restore the data. Otherwise, the IoTDB data that is generated after the data backup and before the data restoration will be lost.

Impact on the System
--------------------

-  During data restoration, user authentication stops and users cannot create new connections.
-  After the data is restored, the data generated after the data backup and before the data restoration is lost.
-  After the data is restored, the IoTDB upper-layer applications need to be started.

Prerequisites
-------------

-  If you need to restore data from a remote HDFS, prepare a standby cluster. If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust must be configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The IoTDB backup file save path is correct.
-  The IoTDB upper-layer applications are stopped.

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

#. In **Restoration Configuration**, choose **IoTDB** > **IoTDB** under **Service Data**.

#. .. _admin_guide_000361__li4457996415256:

   Set **Path Type** of **IoTDB** to a backup directory type.

   The following backup directory types are supported:

   **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

   If you select this option, configure the following parameters:

   -  **Source NameService Name**: indicates the NameService name of the backup data cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.
   -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
   -  **Source Active NameNode IP Address**: indicates the service plane IP address of the active NameNode in the standby cluster.
   -  **Source Standby NameNode IP Address**: indicates the service plane IP address of the standby NameNode in the standby cluster.
   -  **Source NameNode RPC Port**: indicates the value of **dfs.namenode.rpc.port** in the HDFS basic configuration of the standby cluster.
   -  **Source Path**: indicates the full path of HDFS directory for storing backup data of the standby cluster, for example, *Backup path/Backup task name_Data source_Task creation time*.
   -  **Recovery Point List**: Click **Refresh** and select an IoTDB directory that has been backed up in the standby cluster.

#. In the **Backup Data** column of the **Data Configuration** page, select one or more pieces of backup data that needs to be restored based on service requirements. In the **Target Path** column, specify the target location after backup data restoration.

   You are advised to set **Target Path** to a new path that is different from the backup path.

#. Set **Force recovery** to **true**, which indicates that all backup data is forcibly restored when a data table with the same name already exists. If the data table contains new data added after backup, the new data will be lost after the data restoration. If you set the parameter to **false**, the restoration task is not executed if a data table with the same name exists.

#. Click **Verify** to check whether the restoration task is configured correctly.

   -  If the queue name is incorrect, the verification fails.
   -  If the specified directory to be restored does not exist, the verification fails.

#. Click **OK**.

#. In the restoration task list, locate the row where the created task is located, and click **Start** in the **Operation** column.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and click **Retry** to execute the task again.
