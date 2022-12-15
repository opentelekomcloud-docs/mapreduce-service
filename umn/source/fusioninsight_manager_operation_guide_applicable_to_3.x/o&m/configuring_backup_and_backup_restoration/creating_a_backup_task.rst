:original_name: admin_guide_000081.html

.. _admin_guide_000081:

Creating a Backup Task
======================

Scenario
--------

You can create backup tasks on FusionInsight Manager. Executing backup tasks backs up related data.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **O&M** > **Backup and Restoration** > **Backup Management**. On the page that is displayed, click **Create**.

#. Set **Backup Object** to **OMS** or the cluster whose data you want to back up.

#. Enter a task name in the **Name** text box.

#. Set **Mode** to **Periodic** or **Manual** as required.

   .. table:: **Table 1** Backup types

      +-----------------------+-----------------------+-------------------------------------------------------------------------------+
      | Type                  | Parameter             | Description                                                                   |
      +=======================+=======================+===============================================================================+
      | Periodic backup       | Start Time            | Indicates the time when a periodic backup task is started for the first time. |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------+
      |                       | Period                | Task execution interval. Value options are **Hours** and **Days**.            |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------+
      |                       | Backup Policy         | The following policies can be selected:                                       |
      |                       |                       |                                                                               |
      |                       |                       | -  Full backup at the first time and subsequent incremental backup            |
      |                       |                       | -  Full backup every time                                                     |
      |                       |                       | -  Full backup once every n times                                             |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------+
      | Manual backup         | N/A                   | You need to manually execute the task to back up data.                        |
      +-----------------------+-----------------------+-------------------------------------------------------------------------------+

#. Set required parameters in the **Configuration** area.

   -  Metadata and service data can be backed up.
   -  For details about how to back up data of different components, see :ref:`Backup and Recovery Management <admin_guide_000198>`.

#. Click **OK** to save the configurations.

#. In the backup task list, you can view the created backup task.

   Locate the row that contains the target backup task, choose **More** > **Back Up Now** in the **Operation** column to execute the task immediately.
