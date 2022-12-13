:original_name: mrs_01_0321.html

.. _mrs_01_0321:

Restoring Metadata
==================

Scenario
--------

Metadata needs to be recovered in the following scenarios:

-  Data is modified or deleted unexpectedly and needs to be restored.
-  After a critical operation (such as an upgrade or critical data adjustment) is performed on metadata components, an exception occurs or the operation does not achieve the expected result. All modules are faulty and become unavailable.
-  Data is migrated to a new cluster.

You can create a metadata restoration task on MRS. The restoration tasks can be created manually only.

.. important::

   -  Data restoration can be performed only when the system version during data backup is consistent with the current system version.
   -  To restore the data when services are normal, manually back up the latest management data first and then restore the data. Otherwise, the data that is generated after the data backup and before the data restoration will be lost.
   -  Use the OMS data and LdapServer data backed up at the same time to restore data. Otherwise, the service and operation may fail.
   -  By default, MRS clusters use DBService to store Hive metadata.

Impact on the System
--------------------

-  Data generated between the backup time and restoration time is lost after data restoration.
-  After the data is restored, the configuration of the components that depend on DBService may expire and these components need to be restarted.

Prerequisites
-------------

-  You have checked whether the data in the OMS and LdapServer backup files is backed up at the same time.
-  You have checked whether the status of the OMS resource and the LdapServer instance is normal. If the status is abnormal, data restoration cannot be performed.
-  You have checked whether the status of the cluster hosts and services is normal. If the status is abnormal, data restoration cannot be performed.
-  You have checked whether the cluster host topologies during data restoration and data backup are the same. If they are different, data restoration cannot be performed and you need to back up data again.
-  You have checked the services added to the cluster during data restoration and data backup are the same. If they are different, data restoration cannot be performed and you need to back up data again.
-  You have checked whether the status of the active and standby DBService instances is normal. If the status is abnormal, data restoration cannot be performed.
-  You have stopped the upper-layer applications depending on the cluster.
-  On MRS console, you have stopped all the NameNode role instances whose data is to be recovered. Other HDFS role instances must be running properly. After data is recovered, the NameNode role instances need to be restarted. The NameNode role instances cannot be accessed before the restart.
-  Check whether NameNode backup files are stored in *Data storage path*\ **/LocalBackup/** on the active management node.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. Check the location of backup data.

   a. On the cluster details page, choose **Backups & Restorations** > **Backups**.
   b. In the row where the specified backup task resides, choose **More** > **View History** in the **Operation** column to display the historical execution records of the backup task. In the displayed window, locate a specified success backup record. In the **Operation** column, click **View Backup Path** to open the task execution logs. Find the following information and view the path:

      -  **Backup Object**: indicates a backup data source.
      -  **Backup Path**: indicates the full path where the backup files are stored.

   c. Select the correct path, and manually copy the full path of backup files in **Backup Path**.

#. Create a restoration task.

   a. On the cluster details page, choose **Backups & Restorations** > **Restorations**.
   b. On the page that is displayed, click **Create Restoration Task**.
   c. Set **Task Name** to the name of the restoration task.

#. Select restoration sources.

   In the **Configuration** area, select the metadata component whose data is to be restored.

#. Set the restoration parameters.

   a. Set **Path Type** to a backup directory type.
   b. The settings vary according to backup directory types:

      -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node. If you select **LocalDir**, you need to set **Source Path** to specify the full path of the backup file. For example, *Data storage path*\ **/LocalBackup/**\ *Backup task name*\ **\_**\ *Task creation time*\ **/**\ *Data source*\ **\_**\ *Task execution time*\ **/**\ *Version number*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
      -  **LocalHDFS**: indicates that the backup files are stored in the HDFS directory of the current cluster. If you select **LocalHDFS**, set the following parameters:

         -  **Source Path**: indicates the full HDFS path of a backup file, for example, *Backup path/Backup task name_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
         -  **Source Instance Name**: indicates the name of NameService corresponding to the backup directory when a restoration task is being executed. The default value is **hacluster**.

   c. Click **OK**.

#. Execute the restoration task.

   In the restoration task list, locate the row where the created task resides, and click **Start** in the **Operation** column.

   -  After the recovery is successful, the progress bar is in green.
   -  After the recovery is successful, the recovery task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and try to execute the task again by clicking **Start**.

#. If the following metadata type is restored, perform the corresponding operations:

   -  If the OMS and LdapServer metadata is restored, go to :ref:`7 <mrs_01_0321__li3654235411916>`.
   -  If DBService data is restored, no further action is required.
   -  If NameNode data is restored, choose **Components** > **HDFS** > **More** > **Restart Service** on the MRS cluster details page. No further action is required.

#. .. _mrs_01_0321__li3654235411916:

   Restart the service for the recovered data to take effect

   a. On the MRS cluster details page, click **Components**.

   b. Choose **LdapServer** > **More** > **Restart Service** and click **OK**. Wait until the LdapServer service is restarted successfully.

   c. Log in to the active management node. For details, see :ref:`Determining Active and Standby Management Nodes of Manager <mrs_01_0086>`.

   d. Run the following command to restart the OMS:

      **sh ${BIGDATA_HOME}/om-0.0.1/sbin/restart-oms.sh**

      The command has been executed successfully if the following information is displayed:

      .. code-block::

         start HA successfully.

   e. On the cluster details page, click **Components**, choose **KrbServer** > **More** > **Synchronize Configuration**. Deselect **Restart the services and instances whose configurations have expired**. Click **Yes** and wait until the KrbServer service configuration is synchronized and restarted successfully.

   f. On the cluster details page, choose **Configuration** > **Synchronize Configuration** in the upper right corner, deselect **Restart the service or instance whose configurations have expired**, and click **Yes**. Wait until the cluster configuration is synchronized successfully.

   g. On the cluster details page, choose **Management Operations** > **Stop All Components** in the upper right corner. After the cluster is stopped, choose **Management Operations** > **Start All Components**, and wait for the cluster to start.
