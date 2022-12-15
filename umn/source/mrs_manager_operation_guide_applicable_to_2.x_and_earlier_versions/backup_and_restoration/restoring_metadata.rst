:original_name: mrs_01_0555.html

.. _mrs_01_0555:

Restoring Metadata
==================

Scenario
--------

You need to restore metadata in the following scenarios: A user modifies or deletes data unexpectedly, data needs to be retrieved, system data becomes abnormal or does not achieve the expected result, all modules are faulty, and data is migrated to a new cluster.

This section describes how to restore metadata on MRS Manager. Only manual restoration tasks are supported.

.. important::

   -  Data restoration can be performed only when the system version is consistent with that during data backup.
   -  To restore the data when services are normal, manually back up the latest management data first and then restore the data. Otherwise, the data that is generated after the data backup and before the data restoration will be lost.
   -  Use the OMS data and LdapServer data backed up at the same time to restore data. Otherwise, the service and operation may fail.
   -  By default, MRS clusters use DBService to store Hive metadata.

Impact on the System
--------------------

-  After the data is restored, the data generated between the backup time and restoration time is lost.
-  After the data is restored, the configuration of the components that depend on DBService may expire and these components need to be restarted.

Prerequisites
-------------

-  The data in the OMS and LdapServer backup files has been backed up at the same time.
-  The status of the OMS resources and the LdapServer instances is normal. If the status is abnormal, data restoration cannot be performed.
-  The status of the cluster hosts and services is normal. If the status is abnormal, data restoration cannot be performed.
-  The cluster host topologies during data restoration and data backup are the same. If the topologies are different, data restoration cannot be performed and you need to back up data again.
-  The services added to the cluster during data restoration and data backup are the same. If the services are different, data restoration cannot be performed and you need to back up data again.
-  The status of the active and standby DBService instances is normal. If the status is abnormal, data restoration cannot be performed.
-  The upper-layer applications depending on the MRS cluster have been stopped.
-  On MRS Manager, you have stopped all the NameNode role instances whose data is to be recovered. Other HDFS role instances are running properly. After data is recovered, the NameNode role instances need to be restarted and cannot be accessed before the restart.
-  You have checked whether NameNode backup files have been stored in the *Data save path*\ **/LocalBackup/** directory on the active management node.

Procedure
---------

#. Check the location of backup data.

   a. On MRS Manager, choose **System** > **Back Up Data**.
   b. In the row where the specified backup task resides, choose **More** > **View History** in the **Operation** column to display the historical execution records of the backup task. In the window that is displayed, select a success record and click **View Backup Path** in the corresponding column to view its backup path information. Find the following information:

      -  **Backup Object**: indicates the backup data source.
      -  **Backup Path**: indicates the full path where backup files are stored.

   c. Select the correct path, and manually copy the full path of backup files in **Backup Path**.

#. Create a restoration task.

   a. On MRS Manager, choose System > Recovery Management.
   b. On the page that is displayed, click **Create Restoration Task**.
   c. Set **Task Name** to the name of the restoration task.

#. Select restoration sources.

   In **Configuration**, select the metadata component whose data is to be restored.

#. Set the restoration parameters.

   a. Set **Path Type** to a backup directory type.
   b. The settings vary according to backup directory types:

      -  **LocalDir**: indicates that the backup files are stored on the local disk of the active management node. If you select **LocalDir**, you need to set **Source Path** to specify the full path of the backup file. For example, *Data storage path*\ **/LocalBackup/**\ *Backup task name*\ **\_**\ *Task creation time*\ **/**\ *Data source*\ **\_**\ *Task execution time*\ **/**\ *Version number*\ **\_**\ *Data source*\ **\_**\ *Task execution time*\ **.tar.gz**.
      -  **LocalHDFS**: indicates that the backup files are stored in the HDFS directory of the current cluster. If you select **SFTP**, set the following parameters:

         -  **Source Path**: indicates the full HDFS path of a backup file. for example, *Backup path/Backup task name_Task creation time/Version_Data source_Task execution time*\ **.tar.gz**.
         -  **Source Instance Name**: indicates the name of NameService corresponding to the backup directory when a restoration task is being executed. The default value is **hacluster**.

   c. Click **OK**.

#. Execute the restoration task.

   In the restoration task list, locate the row where the created task resides, and click **Start** in the **Operation** column.

   -  After the restoration is successful, the progress bar is in green.
   -  After the restoration is successful, the restoration task cannot be executed again.
   -  If the restoration task fails during the first execution, rectify the fault and try to execute the task again by clicking **Start**.

#. Determine what metadata has been restored.

   -  If the OMS and LdapServer metadata is restored, go to :ref:`7 <mrs_01_0555__en-us_topic_0035271577_li3654235411916>`.
   -  If DBService data is restored, no further action is required.
   -  Restore NameNode data. On MRS Manager, choose **Services > HDFS > More > Restart Service**. The task is complete.

#. .. _mrs_01_0555__en-us_topic_0035271577_li3654235411916:

   Restarting Manager for the recovered data to take effect

   a. In MRS Manager, Choose **LdapServer** > **More** > **Restart Service** and click **OK**. Wait until the LdapServer service is restarted successfully.

   b. Log in to the active management node. For details, see :ref:`Determining Active and Standby Management Nodes of Manager <mrs_01_0086>`.

   c. Run the following command to restart OMS:

      **sh ${BIGDATA_HOME}/om-0.0.1/sbin/restart-oms.sh**

      The command has been executed successfully if the following information is displayed:

      .. code-block::

         start HA successfully.

   d. On MRS Manager, choose **KrbServer > More > Synchronize Configuration**. Do not select Restart the services and instances whose configuration has expired. Click **OK** and wait until the KrbServer service configuration is synchronized and restarted successfully.

   e. Choose **Services > More > Synchronize Configuration**. Do not select Restart the services and instances whose configuration has expired. Click **OK** and wait until the cluster is configured and synchronized successfully.

   f. Choose **Services > More > Stop Cluster**. After the cluster is stopped, choose **Services > More> Start Cluster**.
