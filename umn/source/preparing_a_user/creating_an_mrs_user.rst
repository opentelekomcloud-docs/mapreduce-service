:original_name: mrs_01_0453.html

.. _mrs_01_0453:

Creating an MRS User
====================

Use `IAM <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0026.html>`__ to implement fine-grained permission control over your MRS. With IAM, you can:

-  Create IAM users under your cloud account for employees based on your enterprise's organizational structure so that each employee is allowed to access MRS resources using their unique security credential (IAM user).
-  Grant only the permissions required for users to perform a specific task.
-  Entrust a cloud account or cloud service to perform efficient O&M on your MRS resources.

If your cloud account does not require IAM users, skip this section.

This section describes the procedure for granting permissions (see :ref:`Figure 1 <mrs_01_0453__fig8523123435310>`).

Process Flow
------------

.. _mrs_01_0453__fig8523123435310:

.. figure:: /_static/images/en-us_image_0000002243727990.png
   :alt: **Figure 1** Process for granting MRS permissions

   **Figure 1** Process for granting MRS permissions

#. .. _mrs_01_0453__li895020818018:

   `Create a user group and assign permissions to it <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0030.html>`__.

   Create a user group on the IAM console, and assign MRS permissions to the group.

#. `Create a user and add it to a user group <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0031.html>`__.

   Create a user on the IAM console and add the user to the group created in :ref:`1. Create a user group and assign permissions to it <mrs_01_0453__li895020818018>`.

#. Log in and verify permissions.

   Log in to the console by using the user created, and verify that the user has the granted permissions.

   -  Choose **Service List** > **MapReduce Service**. Then click **Create** **Cluster** on the MRS console. If a message appears indicating that you have insufficient permissions to perform the operation, the **MRS ReadOnlyAccess** policy has already taken effect.
   -  Choose any other service in **Service List**. If a message appears indicating that you have insufficient permissions to access the service, the **MRS ReadOnlyAccess** policy has already taken effect.

MRS Permission Description
--------------------------

By default, new IAM users do not have any permissions. To assign permissions to a user, add the user to one or more groups and assign permissions policies or roles to these groups. The user then inherits permissions from the groups it is a member of and can perform specified operations on cloud services based on the permissions.

MRS is a project-level service deployed and accessed in specific physical regions. To assign permissions to a user group, specify **Scope** as **Region-specific projects** and select projects in the corresponding region for the permissions to take effect. If **All projects** is selected, the permissions will take effect for the user group in all region-specific projects. When accessing MRS, the users need to switch to a region where they have been authorized to use the MRS service.

You can grant users permissions by using roles and policies.

-  Roles: A type of coarse-grained authorization mechanism that defines permissions related to user responsibilities. This mechanism provides only a limited number of service-level roles for authorization. When using roles to grant permissions, you need to also assign other roles on which the permissions depend to take effect. However, roles are not an ideal choice for fine-grained authorization and secure access control.
-  Policies: A type of fine-grained authorization mechanism that defines permissions required to perform operations on specific cloud resources under certain conditions. This mechanism allows for more flexible policy-based authorization, meeting requirements for secure access control. For example, you can grant MRS users only the permissions for performing specified operations on MRS clusters, such as creating a cluster and querying a cluster list rather than deleting a cluster. Most policies define permissions based on APIs.

:ref:`Table 1 <mrs_01_0453__en-us_topic_0264277873_table13757124105911>` lists all the system policies supported by MRS.

.. _mrs_01_0453__en-us_topic_0264277873_table13757124105911:

.. table:: **Table 1** MRS system policies

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Policy                | Description                                                                                                                              | Type                  |
   +=======================+==========================================================================================================================================+=======================+
   | MRS FullAccess        | Administrator permissions for MRS. Users granted these permissions can operate and use all MRS resources.                                | Fine-grained policy   |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MRS CommonOperations  | Common user permissions for MRS. Users granted these permissions can use MRS but cannot add or delete resources.                         | Fine-grained policy   |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MRS ReadOnlyAccess    | Read-only permission for MRS. Users granted these permissions can only view MRS resources.                                               | Fine-grained policy   |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MRS Administrator     | Permissions:                                                                                                                             | RBAC policy           |
   |                       |                                                                                                                                          |                       |
   |                       | -  All operations on MRS                                                                                                                 |                       |
   |                       | -  Users with permissions of this policy must also be granted permissions of the **Tenant Guest** and **Server Administrator** policies. |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

:ref:`Table 2 <mrs_01_0453__en-us_topic_0264277873_table64841036185016>` lists the common operations supported by each system-defined policy or role of MRS. Select the policies or roles as required.

.. _mrs_01_0453__en-us_topic_0264277873_table64841036185016:

.. table:: **Table 2** Common operations supported by each system-defined policy

   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Operation                         | MRS FullAccess | MRS CommonOperations | MRS ReadOnlyAccess | MRS Administrator |
   +===================================+================+======================+====================+===================+
   | Creating a cluster                | Y              | x                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Resizing a cluster                | Y              | x                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Upgrading node specifications     | Y              | x                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Deleting a cluster                | Y              | x                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying cluster details          | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a cluster list           | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Configuring an auto scaling rule  | Y              | x                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a host list              | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying operation logs           | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Creating and executing a job      | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Stopping a job                    | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Deleting a single job             | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Deleting jobs in batches          | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying job details              | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a job list               | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Creating a folder                 | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Deleting a file                   | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a file list              | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Operating cluster tags in batches | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Creating a single cluster tag     | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Deleting a single cluster tag     | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a resource list by tag   | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying cluster tags             | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Accessing Manager                 | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying a patch list             | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Installing a patch                | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Uninstalling a patch              | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Authorizing O&M channels          | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Sharing O&M channel logs          | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying an alarm list            | Y              | Y                    | Y                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Subscribing to alarm notification | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Submitting an SQL statement       | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Querying SQL results              | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
   | Canceling an SQL execution task   | Y              | Y                    | x                  | Y                 |
   +-----------------------------------+----------------+----------------------+--------------------+-------------------+
