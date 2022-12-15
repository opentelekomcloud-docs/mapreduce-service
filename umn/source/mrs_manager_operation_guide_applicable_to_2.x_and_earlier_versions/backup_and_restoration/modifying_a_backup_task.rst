:original_name: mrs_01_0558.html

.. _mrs_01_0558:

Modifying a Backup Task
=======================

Scenario
--------

This section describes how to modify the parameters of a created backup task on MRS Manager to meet changing service requirements. The parameters of restoration tasks can be viewed but not modified.

Impact on the System
--------------------

After a backup task is modified, the new parameters take effect when the task is executed next time.

Prerequisites
-------------

-  A backup task has been created.
-  A new backup task policy has been planned based on the actual situation.

Procedure
---------

#. On MRS Manager, choose **System** > **Back Up Data**.
#. In the task list, locate a specified task, click **Modify** in the **Operation** column to go to the configuration modification page.
#. Modify the following parameters on the displayed page:

   -  Manual backup:

      -  Target Path
      -  Max Number of Backup Copies

   -  Periodic backup:

      -  Started
      -  Period
      -  Target Path
      -  Max Number of Backup Copies

      .. note::

         -  When **Path Type** is set to **LocalHDFS**, **Target Path** is valid for modifying a backup task.
         -  After you change the value of **Target Path** for a backup task, full backup is performed by default when the task is executed for the first time.

#. Click **OK**.
