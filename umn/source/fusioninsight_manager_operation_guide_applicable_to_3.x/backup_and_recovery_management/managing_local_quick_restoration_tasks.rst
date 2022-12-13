:original_name: admin_guide_000229.html

.. _admin_guide_000229:

Managing Local Quick Restoration Tasks
======================================

Scenario
--------

When DistCp is used to back up data, the backup snapshot is saved to HDFS of the active cluster. FusionInsight Manager supports using the local snapshot for quick data restoration, requiring less time than restoring data from the standby cluster.

Use FusionInsight Manager and the snapshots on HDFS of the active cluster to create a local quick restoration task and execute the task.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. In the backup task list, locate a created task and click **Restore** in the **Operation** column.

#. Check whether the system displays "No data is available for quick restoration. Create a task on the restoration management page to restore data".

   -  If yes, click **OK** to close the dialog box. No backup data snapshot is created in the active cluster, and no further action is required.
   -  If no, go to :ref:`Step 4 <admin_guide_000229__en-us_topic_0046736777_q_rec_set>` to create a local quick restoration task.

   .. note::

      Metadata does not support quick restoration.

#. .. _admin_guide_000229__en-us_topic_0046736777_q_rec_set:

   Set **Name** to the name of the local quick restoration task.

#. Set **Configuration** to a data source.

#. Set **Recovery Point List** to a recovery point that contains the backup data.

#. Set **Queue Name** to the name of the Yarn queue used in the task execution. The name must be the same as the name of the queue that is running properly in the cluster.

#. Set **Data Configuration** to the object to be recovered.

#. Click **Verify**, and wait for the system to display "The restoration task configuration is verified successfully."

#. Click **OK**.

#. In the restoration task list, locate a created task and click **Start** in the **Operation** column to execute the restoration task.

   After the task is complete, **Task Status** of the task is displayed as **Successful**.
