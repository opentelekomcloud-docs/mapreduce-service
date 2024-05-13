:original_name: admin_guide_000148.html

.. _admin_guide_000148:

Managing Roles
==============

Scenario
--------

MRS Manager supports a maximum of 5000 roles (including system built-in roles but excluding roles automatically created by tenants). Based on different service requirements, you need to create and manage different roles on MRS Manager and perform authorization management for MRS Manager and components using roles.

Prerequisites
-------------

-  You have learned service requirements.
-  You have logged in to MRS Manager.

.. _admin_guide_000148__section2095713912713:

Creating a Role
---------------

#. Choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and fill in **Role Name** and **Description**.

   The role name consists of 3 to 50 characters, including digits, letters, and underscores (_). It cannot be the same as an existing role name in the system.

#. In the **Configure Resource Permission** area, click the cluster whose permissions are to be added and select service permissions for the role.

   When setting permissions for a component, enter a resource name in the search text box in the upper right corner and click the search icon to view the search result.

   The search result contains only directories, but not subdirectories. Search by keyword supports fuzzy match and is case-insensitive.

   .. note::

      -  For components (except HDFS and Yarn) for which Ranger authorization has been enabled, the permissions of non-default roles on Manager do not take effect. You need to configure Ranger policies to assign permissions to user groups.
      -  If the resource requests of HDFS and Yarn are beyond the Ranger policies, the ACL rules of the components still take effect.
      -  A maximum of 1000 permissions can be set for a component at a time.

#. Click **OK**.

Modifying Role Information
--------------------------

Locate the row that contains the target role and click **Modify**.

Exporting Role Information
--------------------------

Click **Export All** to export all role information at a time in **TXT** or **CSV** format.

The exported role information contains the role name, description, and whether the role is the default role.

Deleting a Role
---------------

Locate the row that contains the target role and click **Delete**. To delete multiple roles in batches, select the target roles and click **Delete** above the role list. A role bound to a user cannot be deleted. To delete such a role, disassociate the role from the user by modifying the user first.

Task Example (Creating a Manager Role)
--------------------------------------

#. Choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and fill in **Role Name** and **Description**.

#. In the **Configure Resource Permission** area, click **Manager** and set permissions for the role.

   Manager permissions:

   -  Cluster

      -  **view** permission: permission to view information on the **Cluster** page and view alarms and events under **O&M** > **Alarm**.
      -  **management** permission: permission for management on the **Cluster** and **O&M** pages.

   -  User

      -  **view** permission: permission to view information on pages under **System** > **Permission**.
      -  **management** permission: permission for management on pages under **System** > **Permission**.

   -  Audit

      **management** permission: permission for management on the **Audit** page.

   -  Tenant

      **management** permission: permission for management on the **Tenant** page and permission to view alarms and events under **O&M** > **Alarm**.

   -  System

      **management** permission: permission for management on all pages except those under **Permission** on the **System** page and permission to view alarms and events under **O&M** > **Alarm**.

#. Click **OK**.
