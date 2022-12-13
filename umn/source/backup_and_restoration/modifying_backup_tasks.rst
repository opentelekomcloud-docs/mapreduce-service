:original_name: mrs_01_0324.html

.. _mrs_01_0324:

Modifying Backup Tasks
======================

Scenario
--------

You can modify the parameters of a created backup task on MRS to meet changing service requirements. The parameters of restoration tasks can only be viewed but cannot be modified.

Impact on the System
--------------------

After a backup task is modified, the new parameters take effect when the task is executed next time.

Prerequisites
-------------

-  A backup task has been created.
-  A new backup task policy has been planned based on the actual situation.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the cluster details page, choose **Backups & Restorations** > **Backups**.
#. In the task list, locate a specified task, click **Modify** in the **Operation** column to go to the configuration modification page.
#. Modify task parameters on the page that is displayed.

   -  The following parameters can be modified for manual backup:

      -  Target Path
      -  Max Number of Backup Copies

   -  The following parameters can be modified for periodic backup:

      -  Started
      -  Period
      -  Target Path
      -  Max Number of Backup Copies

      .. note::

         -  When **Path Type** is set to **LocalHDFS**, **Target Path** is valid for modifying a backup task.
         -  After you change the value of **Target Path** for a backup task, full backup is performed by default when the task is executed for the first time.

#. Click **OK**.
