:original_name: mrs_01_0345.html

.. _mrs_01_0345:

Creating a User
===============

Scenario
--------

This section describes how to create users on Manager based on site requirements and specify their operation permissions to meet service requirements.

Up to 1000 users can be created on Manager.

If a new password policy needs to be used for a new user's password, follow instructions in :ref:`Modifying a Password Policy <mrs_01_0353>` to modify the password policy and then perform the following operations to create a user.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Creating a User <admin_guide_000137>`.

Prerequisites
-------------

-  Administrators have learned service requirements and created roles and role groups required by service scenarios.
-  You have obtained a cluster with Kerberos authentication enabled or a common cluster with the EIP function enabled.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Manage User**.

#. Above the user list, click **Create User**.

#. Configure parameters as prompted and enter a username in **Username**.

   .. note::

      -  A username that differs only in alphabetic case from an existing username is not allowed. For example, if **User1** has been created, you cannot create **user1**.
      -  When you use the user you created, enter the exactly correct username, which is case-sensitive.
      -  **Username** is mandatory and contains 3 to 20 characters. Only digits, letters, and underscores (_) are allowed.
      -  **root**, **omm**, and **ommdba** are reserved system user. Select another username.

#. Set **User Type** to either **Human-machine** or **Machine-machine**.

   -  **Human-machine** user: used for MRS Manager O&M scenarios and component client operation scenarios. If you select this user type, you need to enter a password and confirm the password in **Password** and **Confirm Password** accordingly.
   -  **Machine-machine** users: used for MRS application development scenarios. If you select this user type, you do not need to enter a password, because the password is randomly generated.

#. In **User Group**, click **Select and Join User Group** to select user groups and add users to them.

   .. note::

      -  If roles have been added to user groups, the users can be granted with permissions of the roles.
      -  If you want to grant new users with Hive permissions, add the users to the Hive group.
      -  If a user needs to manage tenant resources, the user group must be assigned the **Manager_tenant** role and the role corresponding to the tenant.
      -  Users created on Manager cannot be added to the user group synchronized using the IAM user synchronization function.

#. In **Primary Group**, select a group as the primary group for users to create directories and files. The drop-down list contains all groups selected in **User Group**.

#. In **Assign Rights by Role**, click **Select and Add Role** to add roles for users based on onsite service requirements.

   .. note::

      -  When you create a user, if permissions of a user group that is granted to the user cannot meet service requirements, you can assign other created roles to the user. It takes 3 minutes to make role permissions granted to the new user take effect.
      -  Adding a role when you create a user can specify the user rights.
      -  A new user can access web UIs of HDFS, HBase, Yarn, Spark, and Hue even when roles are not assigned to the user.

#. In **Description**, provide description based on onsite service requirements.

   **Description** is optional.

#. Click **OK**.

   If a new user is used in the MRS cluster for the first time, for example, used for logging in to MRS Manager or using the cluster client, the password must be changed. For details, see :ref:`Changing the Password of an Operation User <mrs_01_0350>`.
