:original_name: mrs_01_1936.html

.. _mrs_01_1936:

Spark SQL Permissions
=====================

SparkSQL Permissions
--------------------

Similar to Hive, Spark SQL is a data warehouse framework built on Hadoop, providing storage of structured data like structured query language (SQL).

MRS supports users, user groups, and roles. Permission must be assigned to roles and then roles are bound to users or user groups. Users can obtain permissions only by binding a role or joining a group that is bound with a role.

.. note::

   -  If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for Spark2x <mrs_01_1860>`.

   -  After Ranger authentication is enabled or disabled on Spark2x, you need to restart Spark2x and download the client again or update the client configuration file **spark/conf/spark-defaults.conf**.

      Enable Ranger authentication: **spark.ranger.plugin.authorization.enable=true**

      Disable Ranger authentication: **spark.ranger.plugin.authorization.enable=false**

Permission Management
---------------------

Spark SQL permission management indicates the permission system for managing and controlling users' operations on databases, to ensure that different users can operate databases separately and securely. A user can operate another user's tables and databases only with the corresponding permissions. Otherwise, operations will be rejected.

Spark SQL permission management integrates the functions of Hive management. The MetaStore service of Hive and the permission granting function on the page are required to enable Spark SQL permission management.

:ref:`Figure 1 <mrs_01_1936__fd3a2b5c226864acd937682b321890f11>` shows the basic architecture of SparkSQL permission management. This architecture includes two parts: granting permissions on the page, and obtaining and judging a service.

-  Granting permissions on the page: Spark SQL only supports granting permissions on the page. On FusionInsight Manager, choose **System** > **Permission** to add or delete a user, user group, or a role, and to grant permissions or cancel permissions.
-  Obtaining and judging a service: When the DDL and DML commands are received from a client, Spark SQL will obtain the client's permissions on database information from MetaStore, and check whether the required permissions are included. If the required permissions are included, continue the execution. If the required permissions are not included, reject the user's operations. After the MetaStore permissions are checked, ACL permission also needs to be checked on HDFS.

.. _mrs_01_1936__fd3a2b5c226864acd937682b321890f11:

.. figure:: /_static/images/en-us_image_0000001296249948.png
   :alt: **Figure 1** Spark SQL permission management architecture

   **Figure 1** Spark SQL permission management architecture

Additionally, Spark SQL provides column and view permissions to meet requirements of different scenarios.

-  Column permission

   Spark SQL permission control consists of metadata permission control and HDFS ACL permission control. When Hive MetaStore automatically synchronizes table permissions to the HDFS ACL, column-level permissions are not synchronized. In other words, a user with partial or all column-level permissions cannot access the entire HDFS file using the HDFS client.

   -  In **spark-sql** mode, users with only column-level permissions cannot access HDFS files. Therefore, they cannot access the columns of the corresponding tables.
   -  In Beeline/JDBCServer mode, permissions are assigned among users, for example, the permissions on the table created by user A are assigned to user B.

      -  **hive.server2.enable.doAs**\ =\ **true** (configured in the **hive-site.xml** file on the Spark server)

         In this case, user B cannot query the information. You need to manually assign the read permission on the file in HDFS.

      -  **hive.server2.enable.doAs**\ =false

         -  Users A and B are connected by Beeline. User B can query the information.
         -  User A creates a table using SQL statements, and user B can query the table in Beeline.

         However, information query is not supported in other scenarios, for example, user A uses Beeline to create a table and user B uses SQL to query the table, or user A uses SQL to create a table and user B uses SQL to query the table. You need to manually assign the read permission on the file in HDFS.

   .. note::

      The **spark** user is an Spark administrator in HDFS ACL permission control. The permission control of the Beeline client user depends only on the metadata permission on Spark.

-  View permission

   View permission indicates the operation permission such as query and modification on the view of a table, regardless of the corresponding permission of a table. Namely, if you have the permission to query the view of a table, the permission to query the table is not mandatory. The view permission is applicable to the whole table but not to the columns.

   Restrictions of view and column permissions on SparkSQL are similar. The following uses the view permission as an example:

   -  In spark-sql mode, if you have only the view permission but not the table permission and do not have the permission to read HDFS, you cannot access the table data stored in HDFS. That is, you cannot query the view of the table.
   -  In Beeline/JDBCServer mode, permissions are assigned among users, for example, the permissions on the view created by user A are assigned to user B.

      -  **hive.server2.enable.doAs**\ =\ **true** (configured in the **hive-site.xml** file on the Spark server)

         In this case, user B cannot query the information. You need to manually assign the read permission on the file in HDFS.

      -  **hive.server2.enable.doAs**\ =false

         -  Users A and B are connected by Beeline. User B can query the information.
         -  User A creates a view using SQL statements, and user B can query the view in Beeline.

         However, information query is not supported in other scenarios. For example, user A uses Beeline to create a view but user B cannot use SQL to query the view, or user A uses SQL to create a view but user B cannot use SQL to query the view. You need to manually assign the read permission on the file in HDFS.

   Permission of operations on the view of a table is as follows:

   -  To create a view, you must have the CREATE permission on the database and the SELECT and SELECT_of_GRANT permissions on the tables.
   -  Creating and describing a view only entail the SELECT permission on the view. Querying views and tables at the same time entails the SELECT permission on other tables. For example, to perform **select \* from v1 join t1**, you must have the SELECT permission on the **v1** view and **t1** table, even through the **v1** view depends on the **t1** table.

      .. note::

         In Beeline/JDBCServer mode, to query a view, you must have the SELECT permission on the tables. In spark-sql mode, to query a view, you must have the SELECT permission on the view and tables.

   -  Deleting and modifying a view entail the permission of owner on the view.

SparkSQL Permission Model
-------------------------

If you want to perform SQL operations using SparkSQL, you must be granted with permissions of SparkSQL databases and tables (include external tables and views). The complete permission model of SparkSQL consists of the meta data permission and HDFS file permission. Permissions required to use a database or a table is just one type of SparkSQL permission.

-  Metadata permissions

   Metadata permissions are controlled at the metadata layer. Similar to traditional relational databases, SparkSQL databases involve the CREATE and SELECT permissions, and tables and columns involve the SELECT, INSERT, UPDATE, and DELETE permissions. SparkSQL also supports the permissions of **OWNERSHIP** and **ADMIN**.

-  Data file permissions (that is, HDFS file permissions)

   SparkSQL database and table files are stored in HDFS. The created databases or tables are saved in the **/user/hive/warehouse** directory of HDFS by default. The system automatically creates subdirectories named after database names and database table names. To access a database or table, you must have the **Read**, **Write** and **Execute** permissions on the corresponding file in HDFS.

To perform various operations on SparkSQL databases or tables, you need to associate the metadata permission and HDFS file permission. For example, to query SparkSQL data tables, you need to associate the metadata permission **SELECT** and HDFS file permissions **Read** and **Execute**.

Using the management function of Manager GUI to manage the permissions of SparkSQL databases and tables, only requires the configuration of metadata permission, and the system will automatically associate and configure the HDFS file permission. In this way, operations on the interface are simplified, and the efficiency is improved.

Usage Scenarios and Related Permissions
---------------------------------------

Creating a database with SparkSQL service requires users to join in the hive group, without granting a role. Users have all permissions on the databases or tables created by themselves in Hive or HDFS. They can create tables, select, delete, insert, or update data, and grant permissions to other users to allow them to access the tables and corresponding HDFS directories and files.

A user can access the tables or database only with permissions. Users' permissions vary depending on different SparkSQL scenarios.

.. table:: **Table 1** SparkSQL scenarios

   +----------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | Typical Scenario                             | Required Permission                                                                                     |
   +==============================================+=========================================================================================================+
   | Using SparkSQL tables, columns, or databases | Permissions required in different scenarios are as follows:                                             |
   |                                              |                                                                                                         |
   |                                              | -  To create a table, the CREATE permission is required.                                                |
   |                                              | -  To query data, the SELECT permission is required.                                                    |
   |                                              | -  To insert data, the INSERT permission is required.                                                   |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | Associating and using other components       | In some scenarios, except the SparkSQL permission, other permissions may be also required. For example: |
   |                                              |                                                                                                         |
   |                                              | Using Spark on HBase to query HBase data in SparkSQL requires HBase permissions.                        |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------+

In some special SparkSQL scenarios, other permissions must be configured separately.

.. table:: **Table 2** SparkSQL scenarios and required permissions

   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scenario                                                                                                                                                                                                                             | Required Permission                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   +======================================================================================================================================================================================================================================+====================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Creating SparkSQL databases, tables, and external tables, or adding partitions to created Hive tables or external tables when data files specified by Hive users are saved to other HDFS directories except **/user/hive/warehouse** | -  The directory must exist, the client user must be the owner of the directory, and the user must have the **Read**, **Write**, and **Execute** permissions on the directory. The user must have the **Read** and **Execute** permissions of all the upper-layer directories of the directory.                                                                                                                                                                                                                                                    |
   |                                                                                                                                                                                                                                      | -  If the Spark version is later than 2, the **Create** permission of the Hive database is required if you want to create a HBase table. However, in Spark 1.5, the **Create** permissions of both the Hive database and HBase namespace are required if you want to create a HBase table.                                                                                                                                                                                                                                                         |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Importing all the files or specified files in a specified directory to the table using load                                                                                                                                          | -  The data source is a Linux local disk, the specified directory exists, and the system user **omm** has read and execute permission of the directory and all its upper-layer directories. The specified file exists, and user **omm** has the **Read** permission on the file and has the **Read** and **Execute** permissions on all the upper-layer directories of the file.                                                                                                                                                                   |
   |                                                                                                                                                                                                                                      | -  The data source is HDFS, the specified directory exists, and the SparkSQL user is the owner of the directory and has the **Read**, **Write**, and **Execute** permissions on the directory and its subdirectories, and has the **Read** and **Execute** permissions on all its upper-layer directories. The specified file exists, and the SparkSQL user is the owner of the file and has the **Read**, **Write**, and **Execute** permissions on the file and has the **Read** and **Execute** permissions on all its upper-layer directories. |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Creating or deleting functions or modifying any database                                                                                                                                                                             | The **ADMIN** permission is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Performing operations on all databases and tables in Hive                                                                                                                                                                            | The user must be added to the **supergroup** user group, and be assigned the **ADMIN** permission.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | After assigning the **Insert** permission on some DataSource tables, assigning the **Write** permission on table directories in HDFS before performing the insert or analyze operation                                               | When the **Insert** permission is assigned to the **spark datasource** table, if the table format is text, CSV, JSON, Parquet, or ORC, the permission on the table directory is not changed. After the **Insert** permission is assigned to the DataSource table of the preceding formats, you need to assign the **Write** permission to the table directories in HDFS separately so that users can perform the insert or analyze operation on the tables.                                                                                        |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
