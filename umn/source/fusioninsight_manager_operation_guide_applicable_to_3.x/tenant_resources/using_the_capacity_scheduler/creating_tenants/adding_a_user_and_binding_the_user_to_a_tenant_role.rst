:original_name: admin_guide_000120.html

.. _admin_guide_000120:

Adding a User and Binding the User to a Tenant Role
===================================================

Scenario
--------

A newly created tenant cannot directly log in to the cluster to access resources. You need to add a user for the tenant on FusionInsight Manager and bind the user to the role of the tenant to assign operation permissions to the user.

Prerequisites
-------------

You have clarified service requirements and created a tenant.

Procedure
---------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User**.

#. If you want to add a user to the system, click **Create**.

   If you want to bind tenant roles to an existing user in the system, locate the row of the user and click **Modify** in the **Operation** column.

   Set user attributes according to :ref:`Table 1 <admin_guide_000120__t2b6451d372c44135bf8473b6b2dc0fd4>`.

   .. _admin_guide_000120__t2b6451d372c44135bf8473b6b2dc0fd4:

   .. table:: **Table 1** User parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================+
      | Username                          | Specifies the current user name. The value can contain 3 to 32 characters, including digits, letters, underscores (_), hyphens (-), and spaces.                                                                                            |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | -  The username cannot be the same as the OS username of any node in the cluster. Otherwise, the user cannot be used.                                                                                                                      |
      |                                   | -  A username that differs only in alphabetic case from an existing username is not allowed. For example, if **User1** has been created, you cannot create **user1**. Enter the correct username when using **User1**.                     |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Type                         | The options are **Human-Machine** and **Machine-Machine**.                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | -  **Human-Machine** user: used for FusionInsight Manager O&M and component client operations. If you select this option, set both **Password** and **Confirm Password** accordingly.                                                      |
      |                                   | -  **Machine-Machine** user: used for application development. If you select this option, the password is randomly generated.                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Password                          | This parameter is mandatory if **User Type** is set to **Human-Machine**.                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | The password must contain 8 to 64 characters of at least four types of the following: uppercase letters, lowercase letters, digits, special characters, and spaces. The password cannot be the username or the username spelled backwards. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | Enter the password again.                                                                                                                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Group                        | In the **User Group** area, click **Add** and select user groups to add the user to the groups.                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | -  If roles have been added to the user groups, the user can be granted the permissions of the roles.                                                                                                                                      |
      |                                   | -  For example, add the user to the Hive user group to assign Hive permissions to the user.                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Primary Group                     | Select a group as the primary group for the user to create directories and files. The drop-down list contains all groups selected in **User Group**.                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Role                              | Click **Add** to bind a tenant role to the user.                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   |    If a user wants to use the resources of tenant **tenant1** and to add or delete sub-tenants for **tenant1**, the user must be bound to both the **Manager_tenant** and **tenant1\_**\ *Cluster ID* roles.                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Indicates the description of the current user.                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.
