:original_name: mrs_01_0559.html

.. _mrs_01_0559:

Viewing Backup and Restoration Tasks
====================================

Scenario
--------

This section describes how to view created backup and restoration tasks and check their running status on MRS Manager.

Procedure
---------

#. On MRS Manager, click **System**.

#. Click **Back Up Data** or **Restore Data**.

#. In the task list, obtain the previous execution result in the **Task Progress** column. Green indicates that the task is executed successfully, and red indicates that the execution fails.

#. In the **Operation** column of a specified task in the task list, choose **More** > **View History** to view the historical record of backup and restoration execution.

   In the displayed window, click **View** in the **Details** column. The task execution logs and paths are displayed.

Related Tasks
-------------

-  Modifying a backup task

   For details, see :ref:`Modifying a Backup Task <mrs_01_0558>`.

-  Viewing a restoration task

   In the **Operation** column of the specified task in the task list, click **View Details** to view the restoration task. You can only view but cannot modify the parameters of a restoration task.

-  Executing a backup or restoration task

   In the task list, locate a specified task and click **Start** in the **Operation** column to start a backup or restoration task that is ready or fails to be executed. Executed restoration tasks cannot be repeatedly executed.

-  Stopping backup tasks

   In the task list, locate a specified task and click **More** > **Stop** in the **Operation** column to stop a backup task that is running.

-  Deleting a backup or restoration task

   In the **Operation** column of the specified task in the task list, choose **More** > **Delete** to delete the backup or restoration task. After a task is deleted, the backup data is retained by default.

-  Suspending a backup task

   In the **Operation** column of the specified task in the task list, choose **More** > **Suspend** to suspend the backup task. Only periodic backup tasks can be suspended. Suspended backup tasks are no longer executed automatically. When you suspend a backup task that is being executed, the task execution stops. To cancel the suspension status of a task, click **More** > **Resume**.
