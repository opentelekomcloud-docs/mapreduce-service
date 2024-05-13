:original_name: admin_guide_000147.html

.. _admin_guide_000147:

Managing User Groups
====================

Scenario
--------

MRS Manager supports a maximum of 5000 user groups (including built-in user groups). You can create and manage different user groups based on service scenarios on MRS Manager. A user group is bound to a role to obtain operation permissions. After a user is added to a user group, the user can obtain the operation permissions of the user group. A user group can be used to classify users and manage multiple users.

Prerequisites
-------------

-  You have learned service requirements and created roles required by service scenarios.
-  You have logged in to MRS Manager.

.. _admin_guide_000147__section205453863818:

Creating a User Group
---------------------

#. Choose **System** > **Permission** > **User Group**.

#. Above the user group list, click **Create User Group**.

#. Set **Group Name** and **Description**.

   The group name contains 1 to 64 characters, including case-insensitive letters, digits, underscores (_), hyphens (-), and spaces. It cannot be the same as an existing user group name in the system.

#. In the **Role** area, click **Add** to select a role and add it.

   .. note::

      -  For components (except HDFS and Yarn) for which Ranger authorization has been enabled, the permissions of non-default roles on Manager do not take effect. You need to configure Ranger policies to assign permissions to user groups.
      -  If the resource requests of HDFS and Yarn are beyond the Ranger policies, the ACL rules of the components still take effect.

#. In the **User** area, click **Add** to select a user and add it.

#. Click **OK**.

   The user group is created.

Viewing User Group Information
------------------------------

By default, all user groups are displayed in the user group list. You can click the arrow on the left of a user group name to view details about the user group, including the user quantity, specific users, and bound roles of the user group.

Modifying Information About a User Group
----------------------------------------

Locate the row that contains the target user group, and click **Modify** to modify its information.

Exporting Information About a User Group
----------------------------------------

Click **Export All** to export all user group information at a time in **TXT** or **CSV** format.

The exported user group information contains the user group name, description, user list, and role list.

Deleting a User Group
---------------------

Locate the row that contains the target user group, and click **Delete**. To delete multiple user groups in batches, select the target user groups and click **Delete** above the user group list. A user group that contains users cannot be deleted. To delete such a user group, delete all its users by modifying the user group first.
