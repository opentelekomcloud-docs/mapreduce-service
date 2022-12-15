:original_name: mrs_01_0421.html

.. _mrs_01_0421:

Creating a User Group
=====================

Scenario
--------

This section describes how to create user groups and specify their operation permissions on MRS Manager. Management of single or multiple users can be unified in the user groups. After being added to a user group, users can obtain operation permissions owned by the user group.

Up to 100 user groups can be created on MRS Manager.

Prerequisites
-------------

Administrators have learned service requirements and created roles required by service scenarios.

Procedure
---------

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Manage User Group**.

#. Above the user group list, click **Create User Group**.

#. Input **Group Name** and **Description**.

   **Group Name** is mandatory and contains 3 to 20 digits, letters, and underscores (_). **Description** is optional.

#. In **Role**, click **Select and Add Role** to select and add specified roles.

   If you do not add the roles, the user group you are creating now does not have the permission to use MRS clusters.

#. Click **OK**. The user group is created.

Related Tasks
-------------

**Modifying a user group**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User Group**.
#. In the row of the user group to be modified, click **Modify**.

   .. note::

      If you change role permissions assigned to the user group, it takes 3 minutes to make new configurations take effect.

#. Click **OK**. The modification is complete.

**Deleting a user group**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User Group**.
#. In the row of the user group to be deleted, click **Delete**.
#. Click **OK**. The user group is deleted.
