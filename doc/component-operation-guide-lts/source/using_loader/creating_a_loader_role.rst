:original_name: mrs_01_1085.html

.. _mrs_01_1085:

Creating a Loader Role
======================

Scenario
--------

This section describes how to create and configure a Loader role on FusionInsight Manager. The Loader role can set Loader administrator permissions, job connections, job groups, and Loader job operation and scheduling permissions.

Prerequisites
-------------

-  The system administrator has understood the service requirements.
-  You have logged in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

Procedure
---------

#. Choose **System** > **Permission** > **Role**.

#. Click **Create Role** and set a role name and enter description.

#. Set permissions. For details, see :ref:`Table 1 <mrs_01_1085__en-us_topic_0000001219230779_tdca350753d074623bd4d18104fcb7da3>`.

   .. note::

      When setting permissions for a role, you cannot set permissions for multiple resources at the same time. If you need to set permissions for multiple resources, set them one by one.

   Loader permissions:

   -  **Admin**: Loader administrator permission

   -  **Job Connector**: connection permission of Loader

   -  **Job Group**: permission to perform operations on Loader job groups. You can set the operation permissions of a specific job in a specified job group, including the **Edit** and **Execute** permissions of the job.

   -  **Job Scheduler**: permission to schedule Loader jobs

      .. _mrs_01_1085__en-us_topic_0000001219230779_tdca350753d074623bd4d18104fcb7da3:

      .. table:: **Table 1** Setting Loader roles

         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Task                                                                                                                                                                                                                                           | Role Authorization                                                                                                         |
         +================================================================================================================================================================================================================================================+============================================================================================================================+
         | Setting the Loader administrator permission                                                                                                                                                                                                    | In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** and select **Admin**.    |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the connection permission of Loader                                                                                                                                                                                                    | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Connector**.  |
         |                                                                                                                                                                                                                                                | b. In the **Permission** column of the specified job link, select **Edit**.                                                |
         | (including the editing, deletion, and reference permissions of Job Connection)                                                                                                                                                                 |                                                                                                                            |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the edit permission for Loader job groups                                                                                                                                                                                              | a. In the **Permission** table, choose **Loader** > **Job Group**.                                                         |
         |                                                                                                                                                                                                                                                | b. In the **Permission** column of the specified job group, select **Edit Group**.                                         |
         | (including modifying the name of a job group, deleting a specified group, creating jobs in a specified group, importing jobs from external systems to a specified group in batches, and migrating jobs from other groups to a specified group) |                                                                                                                            |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the edit permission for all jobs in a Loader job group                                                                                                                                                                                 | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Group**.      |
         |                                                                                                                                                                                                                                                | b. In the **Permission** column of the specified job group, select **Edit Job**.                                           |
         | (including the permission to edit all existing or new jobs in the group)                                                                                                                                                                       |                                                                                                                            |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the execution permission for all jobs in the Loader job group                                                                                                                                                                          | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Group**.      |
         |                                                                                                                                                                                                                                                | b. In the **Permission** column of the specified job group, select **Execute Job**.                                        |
         | (including the execution permission on all existing or new jobs in the group)                                                                                                                                                                  |                                                                                                                            |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the edit permission for Loader jobs                                                                                                                                                                                                    | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Group**.      |
         |                                                                                                                                                                                                                                                | b. Select a job group.                                                                                                     |
         | (including editing, deleting, copying, and exporting jobs)                                                                                                                                                                                     | c. In the **Permission** column of the specified job, select **Edit**.                                                     |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the execution permission for Loader jobs                                                                                                                                                                                               | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Group**.      |
         |                                                                                                                                                                                                                                                | b. Select a job group.                                                                                                     |
         | (including permissions to start and stop jobs and view historical records)                                                                                                                                                                     | c. In the **Permission** column of the specified job, select **Execute**.                                                  |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for scheduling Loader jobs                                                                                                                                                                                              | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Loader** > **Job Scheduling**. |
         |                                                                                                                                                                                                                                                | b. In the **Permission** column of the specified job scheduling row, select **Edit**.                                      |
         | (including the editing, deletion, and validation permissions of Scheduler)                                                                                                                                                                     |                                                                                                                            |
         +------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+

      .. note::

         a. In addition to **Admin**, the preceding permissions are configured only for inventory resource information.
         b. Users without the preceding roles can also create tasks, groups, and connectors, but cannot perform operations on inventory resources.

#. Click **OK**, and return to the **Role** page.
