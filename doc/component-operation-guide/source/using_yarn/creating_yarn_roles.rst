:original_name: mrs_01_0853.html

.. _mrs_01_0853:

Creating Yarn Roles
===================

Scenario
--------

This section describes how to create and configure a Yarn role. The Yarn role can be assigned with Yarn administrator permission and manage Yarn queue resources.

.. note::

   If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. Refer to :ref:`Adding a Ranger Access Permission Policy for Yarn <mrs_01_1859>` for clusters of MRS 3.\ *x* or later.

Prerequisites
-------------

-  The system administrator has understood the service requirements.
-  You have logged in to Manager.

Procedure
---------

For versions earlier than MRS 3.x, perform the following operations:

#. Choose **System** > **Manage Role** > **Create Role**.

#. Click **Create Role** and fill in **Role Name** and **Description**.

#. Set permissions. For details, see :ref:`Table 1 <mrs_01_0853__t5453ec62e4fa409ab89e13e8c65f7f7b>`.

   Yarn permissions:

   -  **Cluster Admin Operations**: Yarn administrator permissions.

   -  **Scheduler Queue**: queue resources management .

      .. _mrs_01_0853__t5453ec62e4fa409ab89e13e8c65f7f7b:

      .. table:: **Table 1** Setting a role

         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Task                                                                        | Operation                                                                                                                                |
         +=============================================================================+==========================================================================================================================================+
         | Setting the Yarn administrator permission                                   | In the **Permission** table, click **Yarn** and select **Cluster Admin Operations**.                                                     |
         |                                                                             |                                                                                                                                          |
         |                                                                             | .. note::                                                                                                                                |
         |                                                                             |                                                                                                                                          |
         |                                                                             |    The Yarn service needs to be restarted to set the Yarn administrator permission so that the saved role configuration can take effect. |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for a user to submit tasks in a specified Yarn queue | a. In the **Permission** table, choose **Yarn** > **Scheduler Queue**.                                                                   |
         |                                                                             | b. In the **Permission** column of the specified queue, select **Submit**.                                                               |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for a user to manage tasks in a specified Yarn queue | a. In the **Permission** table, choose **Yarn** > **Scheduler Queue**.                                                                   |
         |                                                                             | b. In the **Permission** column of the specified queue, select **Admin**.                                                                |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+

   If the Yarn role contains the **Submit** or **Manage** permission of a parent queue, the sub-queue inherits the permission by default, that is, the **Submit** or **Manage** permission is automatically added for the sub-queue. Permissions inherited by sub-queues will not be displayed as selected in the **Configure Resource Permission** table.

   If you select only the **Submit** permission of a parent queue when setting the Yarn role, you need to manually specify the queue name when submitting tasks as a user with the permission of this role. Otherwise, when the parent queue has multiple sub-queues, the system does not automatically determine the queue to which the task is submitted and therefore submits the task to the **default** queue.

#. Click **OK**.

For MRS 3.\ *x* or later, perform the following operations:

#. Choose System > Permission > Role.

#. Click **Create Role** and set a role name and enter description.

#. Refer :ref:`Table 2 <mrs_01_0853__table16354521181114>` to configure resource permissions for roles.

   Yarn permissions:

   -  Cluster management: Yarn administrator permissions.

   -  Queue scheduling: queue resource management.

      .. _mrs_01_0853__table16354521181114:

      .. table:: **Table 2** Setting a role

         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Task                                                                        | Operation                                                                                                                                |
         +=============================================================================+==========================================================================================================================================+
         | Setting the Yarn administrator permission                                   | In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Yarn** > **Cluster Management**.                |
         |                                                                             |                                                                                                                                          |
         |                                                                             | .. note::                                                                                                                                |
         |                                                                             |                                                                                                                                          |
         |                                                                             |    The Yarn service needs to be restarted to set the Yarn administrator permission so that the saved role configuration can take effect. |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for a user to submit tasks in a specified Yarn queue | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Yarn** > **Scheduling Queue** > **root**.    |
         |                                                                             | b. In the **Permission** column of the specified queue, select **Submit**.                                                               |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for a user to manage tasks in a specified Yarn queue | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Yarn** > **Scheduling Queue** > **root**.    |
         |                                                                             | b. In the **Permission** column of the specified queue, select **Manage**.                                                               |
         +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+

   If the Yarn role contains the **Submit** or **Manage** permission of a parent queue, the sub-queue inherits the permission by default, that is, the **Submit** or **Manage** permission is automatically added for the sub-queue. Permissions inherited by sub-queues will not be displayed as selected in the **Configure Resource Permission** table.

   If you select only the **Submit** permission of a parent queue when setting the Yarn role, you need to manually specify the queue name when submitting tasks as a user with the permission of this role. Otherwise, when the parent queue has multiple sub-queues, the system does not automatically determine the queue to which the task is submitted and therefore submits the task to the **default** queue.

#. Click **OK**.
