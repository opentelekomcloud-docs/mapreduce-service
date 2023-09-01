:original_name: admin_guide_000231.html

.. _admin_guide_000231:

Viewing Backup and Restoration Tasks
====================================

Scenario
--------

This section describes how to view created backup and recovery tasks and check their running status on FusionInsight Manager.

Prerequisites
-------------

You have logged in to FusionInsight Manager. For details, see :ref:`Logging In to FusionInsight Manager <admin_guide_000004>`.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration**.

#. Click **Backup Management** or **Restoration Management**.

#. In the task list, obtain the previous execution result in the **Task Status** and **Task Progress** column. Green indicates that the task is executed successfully, and red indicates that the execution fails.

#. In the **Operation** column of a specified task in the task list, choose **More** > **View History** or click **View History** to view the historical record of backup and restoration task execution.

   In the displayed window, click |image1| before a specified record to display log information about the execution.

Related Tasks
-------------

-  Starting a backup or restoration task

   In the task list, locate a specified task and choose **More** > **Back Up Now** or click **Start** in the **Operation** column to start a backup or restoration task that is ready or fails to be executed. Executed restoration tasks cannot be repeatedly executed.

-  Stopping a backup or restoration task

   In the task list, locate a specified task and choose **More** > **Stop** or click **Stop** in the **Operation** column to stop a backup or restoration task that is running. After the task is successfully stopped, its **Task Status** changes to **Stopped**.

-  Deleting a backup or restoration task

   In the task list, locate a specified task and choose **More** > **Delete** or click **Delete** in the **Operation** column to delete a backup or restoration task. Backup data will be reserved by default after a task is deleted.

-  Suspending a backup task

   In the task list, locate a specified task and choose **More** > **Suspend** in the **Operation** column to suspend a backup task. Only periodic backup tasks can be suspended. Suspended backup tasks are no longer executed automatically. When you suspend a backup task that is being executed, the task execution stops. To resume a task, choose **More** > **Resume**.

.. |image1| image:: /_static/images/en-us_image_0000001392254858.png
