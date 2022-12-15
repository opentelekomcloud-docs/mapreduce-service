:original_name: mrs_01_24044.html

.. _mrs_01_24044:

Default Users of Clusters with Kerberos Authentication Enabled
==============================================================

User Classification
-------------------

The MRS cluster provides the following three types of users. Users are advised to periodically change the passwords. It is not recommended to use the default passwords.

+-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
| User Type                         | Description                                                                                                       |
+===================================+===================================================================================================================+
| System user                       | -  User created on Manager for MRS cluster O&M and service scenarios. There are two types of users:               |
|                                   |                                                                                                                   |
|                                   |    -  **Human-machine** user: used for Manager O&M scenarios and component client operation scenarios.            |
|                                   |    -  **Machine-machine** user: used for MRS cluster application development scenarios.                           |
|                                   |                                                                                                                   |
|                                   | -  User who runs OMS processes.                                                                                   |
+-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
| Internal system user              | Internal user who performs process communications, saves user group information, and associates user permissions. |
+-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
| Database user                     | -  User who manages OMS database and accesses data.                                                               |
|                                   | -  User who runs the database of service components (Hive, Hue, Loader, and DBService)                            |
+-----------------------------------+-------------------------------------------------------------------------------------------------------------------+

System User
-----------

.. note::

   -  User **Idap** of the OS is required in the MRS cluster. Do not delete this account. Otherwise, the cluster may not work properly. Password management policies are maintained by the operation users.
   -  Reset the passwords when you change the passwords of user **ommdba** and user **omm** for the first time. Change the passwords periodically after retrieving them.

+-----------------------------------------+-----------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
| Type                                    | Username        | Initial Password                                   | Description                                                                                                                              |
+=========================================+=================+====================================================+==========================================================================================================================================+
| System administrator of the MRS cluster | admin           | Specified by the user during the cluster creation. | Manager administrator                                                                                                                    |
|                                         |                 |                                                    |                                                                                                                                          |
|                                         |                 |                                                    | with the following permissions:                                                                                                          |
|                                         |                 |                                                    |                                                                                                                                          |
|                                         |                 |                                                    | -  Common HDFS and ZooKeeper user permissions.                                                                                           |
|                                         |                 |                                                    | -  Permissions to submit and query MapReduce and Yarn tasks, manage Yarn queues, and access the Yarn web UI.                             |
|                                         |                 |                                                    | -  Permissions to submit, query, activate, deactivate, reassign, delete topologies, and operate all topologies of the Storm service.     |
|                                         |                 |                                                    | -  Permissions to create, delete, authorize, reassign, consume, write, and query topics of the Kafka service.                            |
+-----------------------------------------+-----------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
| MRS cluster node OS user                | omm             | Randomly generated by the system.                  | Internal running user of the MRS cluster system. This user is an OS user generated on all nodes and does not require a unified password. |
+-----------------------------------------+-----------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
| MRS cluster node OS user                | root            | Set by the user.                                   | User for logging in to the node in the MRS cluster. This user is an OS user generated on all nodes.                                      |
+-----------------------------------------+-----------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+

Internal System Users
---------------------

.. note::

   Do not delete the following internal system users. Otherwise, the cluster or components may not work properly.

+------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Type                   | Default User    | Initial Password | Description                                                                                                                   |
+========================+=================+==================+===============================================================================================================================+
| Component running user | hdfs            | Hdfs@123         | This user is the HDFS system administrator and has the following permissions:                                                 |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  | #. File system operation permissions:                                                                                         |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  |    -  Views, modifies, and creates files.                                                                                     |
|                        |                 |                  |    -  Views and creates directories.                                                                                          |
|                        |                 |                  |    -  Views and modifies the groups where files belong.                                                                       |
|                        |                 |                  |    -  Views and sets disk quotas for users.                                                                                   |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  | #. HDFS management operation permissions:                                                                                     |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  |    -  Views the web UI status.                                                                                                |
|                        |                 |                  |    -  Views and sets the active and standby HDFS status.                                                                      |
|                        |                 |                  |    -  Enters and exits the HDFS in security mode.                                                                             |
|                        |                 |                  |    -  Checks the HDFS file system.                                                                                            |
+------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------+
|                        | hbase           | Hbase@123        | This user is the HBase system administrator and has the following permissions:                                                |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  | -  Cluster management permission: **Enable** and **Disable** operations on tables to trigger MajorCompact and ACL operations. |
|                        |                 |                  | -  Grants and revokes permissions, and shuts down the cluster.                                                                |
|                        |                 |                  | -  Table management permission: Creates, modifies, and deletes tables.                                                        |
|                        |                 |                  | -  Data management permission: Reads and writes data in tables, column families, and columns.                                 |
|                        |                 |                  | -  Accesses the HBase web UI.                                                                                                 |
+------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------+
|                        | mapred          | Mapred@123       | This user is the MapReduce system administrator and has the following permissions:                                            |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  | -  Submits, stops, and views the MapReduce tasks.                                                                             |
|                        |                 |                  | -  Modifies the Yarn configuration parameters.                                                                                |
|                        |                 |                  | -  Accesses the Yarn and MapReduce web UI.                                                                                    |
+------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------+
|                        | spark           | Spark@123        | This user is the Spark system administrator and has the following permissions:                                                |
|                        |                 |                  |                                                                                                                               |
|                        |                 |                  | -  Accesses the Spark web UI.                                                                                                 |
|                        |                 |                  | -  Submits Spark tasks.                                                                                                       |
+------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------+

User Group Information
----------------------

+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Default User Group    | Description                                                                                                                                                                                                                    |
+=======================+================================================================================================================================================================================================================================+
| hadoop                | Users added to this user group have the permission to submit tasks to all Yarn queues.                                                                                                                                         |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| hbase                 | Common user group. Users added to this user group will not have any additional permission.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| hive                  | Users added to this user group can use Hive.                                                                                                                                                                                   |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| spark                 | Common user group. Users added to this user group will not have any additional permission.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| supergroup            | Users added to this user group can have the administrator permission of HBase, HDFS, and Yarn and can use Hive.                                                                                                                |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| check_sec_ldap        | Used to test whether the active LDAP works properly. This user group is generated randomly in a test and automatically deleted after the test is complete. This is an internal system user group used only between components. |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_tenant        | Tenant system user group, which is an internal system user group used only between components.                                                                                                                                 |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| System_administrator  | MRS cluster system administrator group, which is an internal system user group used only between components.                                                                                                                   |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_viewer        | MRS Manager system viewer group, which is an internal system user group used only between components.                                                                                                                          |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_operator      | MRS Manager system operator group, which is an internal system user group used only between components.                                                                                                                        |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_auditor       | MRS Manager system auditor group, which is an internal system user group used only between components.                                                                                                                         |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Manager_administrator | MRS Manager system administrator group, which is an internal system user group used only between components.                                                                                                                   |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| compcommon            | Internal system group for accessing public resources in a cluster. All system users and system running users are added to this user group by default.                                                                          |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| default_1000          | User group created for tenants, which is an internal system user group used only between components.                                                                                                                           |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| kafka                 | Kafka common user group. Users added to this group need to be granted with read and write permission by users in the **kafkaadmin** group before accessing the desired topics.                                                 |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| kafkasuperuser        | Users added to this group have permissions to read data from and write data to all topics.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| kafkaadmin            | Kafka administrator group. Users added to this group have the permissions to create, delete, authorize, as well as read from and write data to all topics.                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| storm                 | Storm common user group. Users added to this group have the permissions to submit topologies and manage their own topologies.                                                                                                  |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| stormadmin            | Storm administrator user group. Users added to this group have the permissions to submit topologies and manage their own topologies.                                                                                           |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| opentsdb              | Common user group. Users added to this user group will not have any additional permission.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| presto                | Common user group. Users added to this user group will not have any additional permission.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| flume                 | Common user group. Users added to this user group will not have any additional permission.                                                                                                                                     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| launcher-job          | MRS internal group, which is used to submit jobs using V2 APIs.                                                                                                                                                                |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| OS User Group | Description                                                                                                                      |
+===============+==================================================================================================================================+
| wheel         | Primary group of MRS internal running user **omm**.                                                                              |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| ficommon      | MRS cluster common group that corresponds to **compcommon** for accessing public resource files stored in the OS of the cluster. |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+

Database User
-------------

MRS cluster system database users include OMS database users and DBService database users.

.. note::

   Do not delete database users. Otherwise, the cluster or components may not work properly.

+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
| Type               | Default User | Initial Password  | Description                                                                                                            |
+====================+==============+===================+========================================================================================================================+
| OMS database       | ommdba       | dbChangeMe@123456 | OMS database administrator who performs maintenance operations, such as creating, starting, and stopping applications. |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
|                    | omm          | ChangeMe@123456   | User for accessing OMS database data.                                                                                  |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
| DBService database | omm          | dbserverAdmin@123 | Administrator of the GaussDB database in the DBService component.                                                      |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
|                    | hive         | HiveUser@         | User for Hive to connect to the DBService database.                                                                    |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
|                    | hue          | HueUser@123       | User for Hue to connect to the DBService database.                                                                     |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
|                    | sqoop        | SqoopUser@        | User for Loader to connect to the DBService database.                                                                  |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
|                    | ranger       | RangerUser@       | User for Ranger to connect to the DBService database.                                                                  |
+--------------------+--------------+-------------------+------------------------------------------------------------------------------------------------------------------------+
