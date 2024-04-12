:original_name: mrs_01_1725.html

.. _mrs_01_1725:

MetaStore Permission Overview
=============================

Constraints: This parameter applies only to the Hive data source.

When multiple HetuEngine clusters are deployed for collaborative computing, the metadata is centrally managed by the management cluster. Data computing is performed in all clusters. The user permission for accessing HetuEngine clusters must be configured in the management cluster. Users who belong to the Hive user group and share the same name are added to all compute instances.

MetaStore Permission
--------------------

Similar to Hive, HetuEngine is a data warehouse framework built on Hadoop, providing storage of structured data like SQL.

Permissions in a cluster must be assigned to roles which are bound to users or user groups. Users can obtain permissions only by binding a role or joining a group that is bound with a role.

Permission Management
---------------------

HetuEngine permission management is performed by the permission system to manage users' operations on the database, ensuring that different users can operate databases independently and securely. A user can operate another user's tables and databases only with the corresponding permissions. Otherwise, operations will be rejected.

HetuEngine permission management integrates the functions of Hive permission management. MetaStore service of Hive and the function of granting permissions on the web page are required to enable the HetuEngine permission management.

-  Granting permissions on the web page: HetuEngine only supports granting permissions on the web page. On Manager, choose **System** > **Permission** to add or delete a user, user group, or a role, and to grant permissions or cancel permissions.
-  Obtaining and judging a service: When the DDL and DML commands are received from the client, HetuEngine will obtain the client user's permissions on database information from MetaStore, and check whether the required permissions are included. If the required permissions have been obtained, the user's operations are allowed. If the permissions are not obtained, the user's operation will be rejected. After the MetaStore permissions are checked, ACL permission also needs to be checked on HDFS.

HetuEngine Permission Model
---------------------------

If a user uses HetuEngine to perform SQL query, the user must be granted with permissions of HetuEngine databases and tables (include external tables and views). The complete permission model of HetuEngine consists of the metadata permission and HDFS file permission. Permissions required to use a database or a table are just one type of HetuEngine permission.

-  Metadata permissions

   Metadata permissions are controlled at the metadata level. Similar to traditional relational databases, the HetuEngine database contains the CREATE and SELECT permissions. Tables and columns contain the SELECT, INSERT, UPDATE, and DELETE permissions. HetuEngine also supports the permissions of OWNERSHIP and ADMIN.

-  Data file permissions (that is, HDFS file permissions)

   HetuEngine database and table files are stored in HDFS. The created databases or tables are saved in the **/user/hive/warehouse** directory of HDFS by default. The system automatically creates subdirectories named after database names and database table names. To access a database or a table, the corresponding file permissions (READ, WRITE, and EXECUTE) on HDFS are required.

To perform various operations on HetuEngine databases or tables, you need to associate the metadata permission and the HDFS file permission. For example, to query HetuEngine data tables, you need to associate the metadata permission SELECT with the READ and EXECUTE permissions on HDFS files.

To use the management function of FusionInsight Manager GUI to manage the permissions of HetuEngine databases and tables, you only need to configure the metadata permission, and the system will automatically associate and configure the HDFS file permission. In this way, operations on the interface are simplified, improving efficiency.

HetuEngine Application Scenarios and Related Permissions
--------------------------------------------------------

A user needs to join in the Hive group if a database is created using the HetuEngine service, and role authorization is not required. Users have all permissions on the databases or tables created by themselves in Hive or HDFS. They can create tables, select, delete, insert, or update data, and grant permissions to other users to allow them to access the tables and corresponding HDFS directories and files.

A user can access the tables or database only with permissions. Permissions required for the user vary depending on different HetuEngine scenarios.

.. table:: **Table 1** Typical HetuEngine scenarios and required permissions

   +------------------------------------------------+-------------------------------------------------------------+
   | Scenario                                       | Required Permission                                         |
   +================================================+=============================================================+
   | Using HetuEngine tables, columns, or databases | Permissions required in different scenarios are as follows: |
   |                                                |                                                             |
   |                                                | -  To create a table, the CREATE permission is required.    |
   |                                                | -  To query data, the SELECT permission is required.        |
   |                                                | -  To insert data, the INSERT permission is required.       |
   +------------------------------------------------+-------------------------------------------------------------+

In some special HetuEngine scenarios, other permissions must be configured separately.

.. table:: **Table 2** Typical HetuEngine authentication scenarios and required permissions

   +----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scenario                                                                                                                                                                                                                         | Required Permission                                                                                                                                                                                                                                                      |
   +==================================================================================================================================================================================================================================+==========================================================================================================================================================================================================================================================================+
   | Creating HetuEngine databases, tables, and foreign tables, or adding partitions to created tables or foreign tables when data files specified by Hive users are saved to other HDFS directories except **/user/hive/warehouse**. | The directory must exist, the client user must be the owner of the directory, and the user must have the READ, WRITE, and EXECUTE permissions on the directory. The user must have the READ and EXECUTE permissions of all the upper-layer directories of the directory. |
   +----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Performing operations on all databases and tables in Hive                                                                                                                                                                        | The user must be added to the **supergroup** user group, and be assigned the ADMIN permission.                                                                                                                                                                           |
   +----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Enabling MetaStore Authentication
---------------------------------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Disable Ranger**.
#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Restart Service**.
#. Restart the compute instance on HSConsole. For details, see :ref:`Managing a HetuEngine Compute Instance <mrs_01_1736>`.
