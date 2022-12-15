:original_name: mrs_01_0561.html

.. _mrs_01_0561:

Default Users of Clusters with Kerberos Authentication Disabled
===============================================================

User Classification
-------------------

The MRS cluster provides the following two types of users. Users are advised to periodically change the passwords. It is not recommended to use the default passwords.

+-----------------------------------+-----------------------------------------------------------------------------------+
| User Type                         | Description                                                                       |
+===================================+===================================================================================+
| System users                      | User who runs OMS processes                                                       |
+-----------------------------------+-----------------------------------------------------------------------------------+
| Database users                    | -  User who manages OMS database and accesses data                                |
|                                   | -  User who runs the database of service components (Hive, Loader, and DBService) |
+-----------------------------------+-----------------------------------------------------------------------------------+

System users
------------

.. note::

   -  User **Idap** of the OS is required in the MRS cluster. Do not delete this account. Otherwise, the cluster may not work properly. Password management policies are maintained by the operation users.
   -  Reset the passwords when you change the passwords of user **ommdba** and user **omm** for the first time. Change the passwords periodically after retrieving them.

+-----------------------------------------+-----------------+---------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| Operation                               | Username        | Initial Password                                  | Description                                                                                                                             |
+=========================================+=================+===================================================+=========================================================================================================================================+
| System administrator of the MRS cluster | admin           | Specified by the user during the cluster creation | -  Default user of MRS Manager to record cluster audit logs for versions earlier than MRS 1.8.0.                                        |
|                                         |                 |                                                   |                                                                                                                                         |
|                                         |                 |                                                   | -  For clusters of 1.8.0 and later versions, the administrator password of MRS Manager is specified by users during cluster creation.   |
|                                         |                 |                                                   |                                                                                                                                         |
|                                         |                 |                                                   |    This user also has the following permissions:                                                                                        |
|                                         |                 |                                                   |                                                                                                                                         |
|                                         |                 |                                                   |    -  Common HDFS and ZooKeeper user permissions.                                                                                       |
|                                         |                 |                                                   |    -  Permissions to submit and query MapReduce and Yarn tasks, manage Yarn queues, and access the Yarn web UI.                         |
|                                         |                 |                                                   |    -  Permissions to submit, query, activate, deactivate, reassign, delete topologies, and operate all topologies of the Storm service. |
|                                         |                 |                                                   |    -  Permissions to create, delete, authorize, reassign, consume, write, and query topics of the Kafka service.                        |
+-----------------------------------------+-----------------+---------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| MRS cluster node OS user                | omm             | Randomly generated by the system                  | Internal running user of the MRS cluster system. This user is an OS user generated on all node and does not require a unified password. |
+-----------------------------------------+-----------------+---------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| MRS cluster node OS user                | root            | Set by the user                                   | User for logging in to the node in the MRS cluster. This user is an OS user generated on all nodes.                                     |
|                                         |                 |                                                   |                                                                                                                                         |
|                                         |                 | .. note::                                         |                                                                                                                                         |
|                                         |                 |                                                   |                                                                                                                                         |
|                                         |                 |    Applicable to clusters of MRS 1.6.2 and later. |                                                                                                                                         |
+-----------------------------------------+-----------------+---------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

User Group Information
----------------------

+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Default User Group    | Description                                                                                                                                                                                                                     |
+=======================+=================================================================================================================================================================================================================================+
| supergroup            | Primary group of user **admin**, which has no additional permissions in the cluster with Kerberos authentication disabled.                                                                                                      |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| check_sec_ldap        | Used to test whether the active LDAP works properly. This user group is generated randomly in a test and automatically deleted after the test is complete. which is an internal system user group used only between components. |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_tenant        | Tenant system user group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                                |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| System_administrator  | MRS cluster system administrator group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                  |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_viewer        | MRS Manager system viewer group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                         |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_operator      | MRS Manager system operator group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                       |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_auditor       | MRS Manager system auditor group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                        |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_administrator | MRS Manager system administrator group, which is an internal system user group used only between components. It is used only in clusters with Kerberos authentication enabled.                                                  |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| compcommon            | MRS cluster internal group, used to access public resources in the cluster. All system users and system running users are added to this user group by default.                                                                  |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| default_1000          | User group created for tenants, which is an internal system user group used only between components.                                                                                                                            |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| launcher-job          | MRS internal group, which is used to submit jobs using V2 APIs.                                                                                                                                                                 |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| OS User Group | Description                                                                                                                      |
+===============+==================================================================================================================================+
| wheel         | Primary group of MRS internal running user **omm**.                                                                              |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| ficommon      | MRS cluster common group that corresponds to **compcommon** for accessing public resource files stored in the OS of the cluster. |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+

Database users
--------------

MRS cluster system database users include OMS database users and DBService database users.

.. note::

   Do not delete database users. Otherwise, the cluster or components may not work properly.

+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
| Operation          | Default User | Initial Password  | Description                                                                                               |
+====================+==============+===================+===========================================================================================================+
| OMS database       | ommdba       | dbChangeMe@123456 | OMS database administrator who performs maintenance operations, such as creating, starting, and stopping. |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
|                    | omm          | ChangeMe@123456   | User for accessing OMS database data                                                                      |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
| DBService database | omm          | dbserverAdmin@123 | Administrator of the GaussDB database in the DBService component                                          |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
|                    | hive         | HiveUser@         | User for Hive to connect to the DBService database                                                        |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
|                    | hue          | HueUser@123       | User for Hue to connect to the DBService database                                                         |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
|                    | sqoop        | SqoopUser@        | User for Loader to connect to the DBService database.                                                     |
+--------------------+--------------+-------------------+-----------------------------------------------------------------------------------------------------------+
