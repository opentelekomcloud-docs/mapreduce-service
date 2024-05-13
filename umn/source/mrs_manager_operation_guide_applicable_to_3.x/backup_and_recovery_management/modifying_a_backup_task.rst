:original_name: admin_guide_000230.html

.. _admin_guide_000230:

Modifying a Backup Task
=======================

Scenario
--------

This section describes how to modify the parameters of a created backup task on MRS Manager to meet changing service requirements. The parameters of restoration tasks can only be viewed but cannot be modified.

Impact on the System
--------------------

After a backup task is modified, the new parameters take effect when the task is executed next time.

Prerequisites
-------------

-  A backup task has been created.
-  A new backup task policy has been planned based on the actual situation.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. In the task list, locate a specified task, click **Configure** in the **Operation** column to go to the configuration modification page.

   On the displayed page, modify the following parameters:

   -  Started
   -  Period
   -  Destination NameService Name
   -  Target NameNode IP Address
   -  Target Path
   -  Max Number of Backup Copies
   -  Maximum Number of Recovery Points
   -  Maximum Number of Maps
   -  Maximum Bandwidth of a Map

   .. note::

      After the **Target Path** parameter of a backup task is modified, this task will be performed as a full backup task for the first time by default.

#. Click **OK** to save the settings.
