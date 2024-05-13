:original_name: mrs_01_0341.html

.. _mrs_01_0341:

Users and Permissions of MRS Clusters
=====================================

Overview
--------

-  **MRS Cluster Users**

   Indicate the security accounts of Manager, including usernames and passwords. These accounts are used to access resources in MRS clusters. Each MRS cluster in which Kerberos authentication is enabled can have multiple users.

-  **MRS Cluster Roles**

   Before using resources in an MRS cluster, users must obtain the access permission which is defined by MRS cluster objects. A cluster role is a set of one or more permissions. For example, the permission to access a directory in HDFS needs to be configured in the specified directory and saved in a role.

Manager provides the user permission management function for MRS clusters, facilitating permission and user management.

-  Permission management: adopts the role-based access control (RBAC) mode. In this mode, permissions are granted by role to form a permission set. After one or more roles are allocated to a user, the user can obtain the permissions of the roles.
-  User management: uses MRS Manager to uniformly manage users, adopts the Kerberos protocol for user identity verification, and employs Lightweight Directory Access Protocol (LDAP) to store user information.

Permission Management
---------------------

Permissions provided by MRS clusters include the O&M permissions of Manager and components (such as HDFS, HBase, Hive, and Yarn). In actual application, permissions must be assigned to each user based on service scenarios. To facilitate permission management, Manager introduces the role function to allow administrators to select and assign specified permissions. Permissions are centrally viewed and managed in permission sets, enhancing user experience.

A role is a logical entity that contains one or more permissions. Permissions are assigned to roles, and users can be granted the permissions by obtaining the roles.

A role can have multiple permissions, and a user can be bound to multiple roles.

-  Role 1: is assigned operation permissions A and B. After role 1 is allocated to users a and b, users a and b can obtain operation permissions A and B.
-  Role 2: is assigned operation permission C. After role 2 is allocated to users c and d, users c and d can obtain operation permission C.
-  Role 3: is assigned operation permissions D and F. After role 3 is allocated to user a, user a can obtain operation permissions D and F.

For example, if an MRS user is bound to the administrator role, the user becomes an administrator of the MRS cluster.

:ref:`Table 1 <mrs_01_0341__te7b79730a8de49dc9a52be8196677697>` lists the roles that are created by default on Manager.

.. _mrs_01_0341__te7b79730a8de49dc9a52be8196677697:

.. table:: **Table 1** Default roles and description

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Default Role          | Description                                                                                                                     |
   +=======================+=================================================================================================================================+
   | default               | Tenant role                                                                                                                     |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Manager_administrator | Manager administrator: This role has the permission to manage MRS Manager.                                                      |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Manager_auditor       | Manager auditor: This role has the permission to view and manage auditing information.                                          |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Manager_operator      | Manager operator: This role has all permissions except tenant, configuration, and cluster management permissions.               |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Manager_viewer        | Manager viewer: This role has the permission to view the information about systems, services, hosts, alarms, and auditing logs. |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | System_administrator  | System administrator: This role has the permissions of Manager administrators and all service administrators.                   |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Manager_tenant        | Manager tenant viewer: This role has the permission to view information on the **Tenant** page on MRS Manager.                  |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------+

When creating a role on Manager, you can perform rights management for Manager and components, as shown in :ref:`Table 2 <mrs_01_0341__t1eebab7f372e49fbb70f1802069f1001>`.

.. _mrs_01_0341__t1eebab7f372e49fbb70f1802069f1001:

.. table:: **Table 2** Manager and component permission management

   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | Permission                        | Description                                                                                   |
   +===================================+===============================================================================================+
   | Manager                           | Manager access and login permission.                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | HBase                             | HBase administrator permission and permission for accessing HBase tables and column families. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | HDFS                              | HDFS directory and file permission.                                                           |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | Hive                              | -  Hive Admin Privilege                                                                       |
   |                                   |                                                                                               |
   |                                   |    Hive administrator permission.                                                             |
   |                                   |                                                                                               |
   |                                   | -  Hive Read Write Privileges                                                                 |
   |                                   |                                                                                               |
   |                                   |    Hive data table management permission to set and manage the data of created tables.        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | Hue                               | Storage policy administrator permissions.                                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+
   | Yarn                              | -  Cluster Admin Operations                                                                   |
   |                                   |                                                                                               |
   |                                   |    Yarn administrator permission.                                                             |
   |                                   |                                                                                               |
   |                                   | -  Scheduler Queue                                                                            |
   |                                   |                                                                                               |
   |                                   |    Queue resource management permission.                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------+

User Management
---------------

MRS clusters that support Kerberos authentication use the Kerberos protocol and LDAP for user management.

-  Kerberos verifies the identity of the user when a user logs in to Manager or uses a component client. Identity verification is not required for clusters with Kerberos authentication disabled.
-  LDAP is used to store user information, including user records, user group information, and permission information.

MRS clusters can automatically update Kerberos and LDAP user data when users are created or modified on Manager. They can also automatically perform user identity verification and authentication and obtain user information when a user logs in to Manager or uses a component client. This ensures the security of user management and simplifies the user management tasks. Manager also provides the user group function for managing one or multiple users by type:

-  A user group is a set of users, which can be used to manage users by type. Users in the system can exist independently or in a user group.
-  After a user is added to a user group to which roles are allocated, the role permission of the user group is assigned to the user.

:ref:`Table 3 <mrs_01_0341__td676ae12a3a64c008ec055b498a52d78>` lists the user groups that are created by default on MRS Manager in MRS 3.x or earlier.

For details about the default user groups displayed on MRS Manager of MRS 3.\ *x* or later, see :ref:`User group <admin_guide_000240__section1031812876>`.

.. _mrs_01_0341__td676ae12a3a64c008ec055b498a52d78:

.. table:: **Table 3** Default user groups and description

   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | User Group     | Description                                                                                                                                                                    |
   +================+================================================================================================================================================================================+
   | hadoop         | Users added to this user group have the permission to submit tasks to all Yarn queues.                                                                                         |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hbase          | Common user group. Users added to this user group will not have any additional permission.                                                                                     |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hive           | Users added to this user group can use Hive.                                                                                                                                   |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | spark          | Common user group. Users added to this user group will not have any additional permission.                                                                                     |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | supergroup     | Users added to this user group can have the administrator permission of HBase, HDFS, and Yarn and can use Hive.                                                                |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | flume          | Common user group. Users added to this user group will not have any additional permission.                                                                                     |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kafka          | Kafka common user group. Users added to this group need to be granted with read and write permission by users in the **kafkaadmin** group before accessing the desired topics. |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kafkasuperuser | Users added to this group have permissions to read data from and write data to all topics.                                                                                     |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kafkaadmin     | Kafka administrator group. Users added to this group have the permissions to create, delete, authorize, as well as read from and write data to all topics.                     |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | storm          | Storm common user group. Users added to this group have the permissions to submit topologies and manage their own topologies.                                                  |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stormadmin     | Storm administrator user group. Users added to this group have the permissions to submit topologies and manage their own topologies.                                           |
   +----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

User **admin** is created by default for MRS clusters with Kerberos authentication enabled and is used for administrators to maintain the clusters.

Process Overview
----------------

In practice, MRS cluster users must understand the service scenarios of big data and plan user permissions. Then, create roles and assign permissions to the roles on MRS Manager to meet service requirements. Manager provides the user group function for administrators to create user groups for managing users of one or multiple service scenarios of the same type.

.. note::

   If a role has the permission of HDFS, HBase, Hive, or Yarn respectively, the role can only use the corresponding functions of the component. To use Manager, the corresponding Manager permission must be added to the role.


.. figure:: /_static/images/en-us_image_0000001349057881.png
   :alt: **Figure 1** Process of creating a user

   **Figure 1** Process of creating a user
