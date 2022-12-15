:original_name: mrs_01_0422.html

.. _mrs_01_0422:

Creating a User
===============

Scenario
--------

This section describes how to create users on MRS Manager based on site requirements and specify their operation permissions to meet service requirements.

Up to 1,000 users can be created on MRS Manager.

If a new password policy needs to be used for a new user's password, follow instructions in :ref:`Modifying a Password Policy <mrs_01_0430>` to modify the password policy and then perform the following operations to create a user.

Prerequisites
-------------

Administrators have learned service requirements and created roles and role groups required by service scenarios.

Procedure
---------

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Manage User**.

#. Above the user list, click **Create User**.

#. Configure parameters as prompted and enter a username in **User Name**.

   .. note::

      -  If a username exists, you cannot create another username that only differs from the existing username in case. For example, if **User1** has been created, you cannot create **user1**.
      -  When you use the user you created, enter the correct username, which is case-sensitive.
      -  **User Name** is mandatory and contains 3 to 20 digits, letters, and underscores (_).
      -  **root**, **omm**, and **ommdba** are reserved system user. Select another username.

#. Set **User Type** to either **Human-Machine** or **Machine-Machine**.

   -  **Human-Machine** users: used for O&M on MRS Manager and operations on component clients. If you select this user type, you need to enter a password and confirm the password in **Password** and **Confirm Password** accordingly.
   -  **Machine-Machine** users: used for MRS application development. If you select this user type, you do not need to enter a password, because the password is randomly generated.

#. In **User Group**, click **Select and Join User Group** to select user groups and add users to them.

   .. note::

      -  If roles have been added to user groups, the users can be granted with permissions of the roles.
      -  If you want to grant new users with Hive permissions, add the users to the Hive group.
      -  If a user needs to manage tenant resources, the user group must be assigned the **Manager_tenant** role and the role corresponding to the tenant.

#. In **Primary Group**, select a group as the primary group for users to create directories and files. The drop-down list contains all groups selected in **User Group**.

#. In **Assign Rights by Role**, click **Select and Add Role** to add roles for users based on service requirements.

   .. note::

      -  When you create a user, if permissions of a user group that is granted to the user cannot meet service requirements, you can assign other created roles to the user. It takes 3 minutes to make role permissions granted to the new user take effect.
      -  Adding a role when you create a user can specify the user rights.
      -  A new user can access WebUIs of HDFS, HBase, Yarn, Spark, and Hue even when roles are not assigned to the user.

#. In **Description**, provide description based on onsite service requirements.

   **Description** is optional.

#. Click **OK**. The user is created.

   If a new user is used in the MRS cluster for the first time, for example, used for logging in to MRS Manager or using the cluster client, the password must be changed. For details, see section **Changing the Password of an Operation User**.
