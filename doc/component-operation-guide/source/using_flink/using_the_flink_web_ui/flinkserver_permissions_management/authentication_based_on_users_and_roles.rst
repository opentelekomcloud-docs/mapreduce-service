:original_name: mrs_01_24049.html

.. _mrs_01_24049:

Authentication Based on Users and Roles
=======================================

This section describes how to create and configure a FlinkServer role on Manager as the system administrator. A FlinkServer role can be configured with FlinkServer administrator permission and the permissions to edit and view applications.

You need to set permissions for the specified user in FlinkServer so that they can update, query, and delete data.

Prerequisites
-------------

The system administrator has planned permissions based on business needs.

Procedure
---------

#. Log in to Manager.

#. Choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and specify **Role Name** and **Description**.

#. Set **Configure Resource Permission**.

   FlinkServer permissions are as follows:

   -  **FlinkServer Admin Privilege**: highest-level permission. Users with the permission can perform service operations on all FlinkServer applications.
   -  **FlinkServer Application**: Users can set **application view** and **applications management** permissions on applications.

   .. table:: **Table 1** Setting a role

      +------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
      | Scenario                                       | Role Authorization                                                                                                                 |
      +================================================+====================================================================================================================================+
      | Setting the administrator operation permission | In **Configure Resource Permission**, choose *Name of the desired cluster* > **Flink** and select **FlinkServer Admin Privilege**. |
      +------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
      | Setting a specified permission on applications | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Flink** > **FlinkServer Application**. |
      |                                                | b. In the **Permission** column, select **application view** or **applications management**.                                       |
      +------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**. Return to role management page.

   .. note::

      After the FlinkServer role is created, create a FlinkServer user and bind the user to the role and user group.
