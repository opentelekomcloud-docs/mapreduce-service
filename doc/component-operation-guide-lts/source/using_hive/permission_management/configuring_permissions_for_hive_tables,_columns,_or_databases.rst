:original_name: mrs_01_0950.html

.. _mrs_01_0950:

Configuring Permissions for Hive Tables, Columns, or Databases
==============================================================

Scenario
--------

You can configure related permissions if you need to access tables or databases created by other users. Hive supports column-based permission control. If a user needs to access some columns in tables created by other users, the user must be granted the permission for columns. The following describes how to grant table, column, and database permissions to users by using the role management function of MRS Manager.

.. note::

   -  You can configure permissions for Hive tables, columns, or databases only in security mode.
   -  If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

Prerequisites
-------------

-  You have obtained a user account with the system administrator permissions, such as **admin**.
-  You have created a role, for example, **hrole**, on Manager by referring to instructions in :ref:`Creating a Hive Role <mrs_01_0949>`. You do not need to set the Hive permission but need to set the permission to submit the HQL command to Yarn for execution.
-  You have created two Hive human-machine users, such as **huser1** and **huser2**, on Manager and added them to the **hive** group. **huser2** has been bound to **hrole**. The **hdb** database has created by user **huser1** and the **htable** table has been created in the database.

Procedure
---------

-  Granting Table Permissions

   Users have complete permission on the tables created by themselves in Hive and the HDFS. To access the tables created by others, they need to be granted the permission. After the Hive metadata permission is granted, the HDFS permission is automatically granted. The procedure for granting a role the permission of querying, inserting, and deleting **htable** data is as follows:

   #. On FusionInsight Manager, choose **System** > **Permission** > **Role**.
   #. Locate the row that contains **hrole**, and click **Modify**.
   #. Choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges**.
   #. Click the name of the specified database **hdb** in the database list. Table **htable** in the database is displayed.
   #. In the **Permission** column of the **htable** table, select **SELECT**, **INSERT**, and **DELETE**.
   #. Click **OK**.

.. note::

   In role management, the procedure for granting a role the permission of querying, inserting, and deleting Hive external table data is the same. After the metadata permission is granted, the HDFS permission is automatically granted.

-  Granting Column Permissions

   Users have all permissions for the tables created by themselves in Hive and HDFS. Users do not have the permission to access the tables created by others. If a user needs to access some columns in tables created by other users, the user must be granted the permission for columns. After the Hive metadata permission is granted, the HDFS permission is automatically granted. The procedure for granting a role the permission of querying and inserting data in **hcol** of **htable** is as follows:

   #. On FusionInsight Manager, choose **System** > **Permission** > **Role**.
   #. Locate the row that contains **hrole**, and click **Modify**.
   #. Choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges**.
   #. In the database list, click the specified database **hdb** to display the **htable** table in the database. Click the **htable** table to display the **hcol** column in the table.
   #. In the **Permission** column of the **hcol** column, select **SELECT** and **INSERT**.
   #. Click **OK**.

.. note::

   In role management, after the metadata permission is granted, the HDFS permission is automatically granted. Therefore, after the column permission is granted, the HDFS ACL permission for all files of the table is automatically granted.

-  Granting Database Permissions

   Users have complete permission on the databases created by themselves in Hive and the HDFS. To access the databases created by others, they need to be granted the permission. After the Hive metadata permission is granted, the HDFS permission is automatically granted. The procedure for granting a role the permission of querying data and creating tables in database **hdb** is as follows. Other types of database operation permission are not supported.

   #. On FusionInsight Manager, choose **System** > **Permission** > **Role**.
   #. Locate the row that contains **hrole**, and click **Modify**.
   #. Choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges**.
   #. In the **Permission** column of the **hdb** database, select **SELECT** and **CREATE**.
   #. Click **OK**.

.. note::

   -  Any permission for a table in the database is automatically associated with the HDFS permission for the database directory to facilitate permission management. When any permission for a table is canceled, the system does not automatically cancel the HDFS permission for the database directory to ensure performance. In this case, users can only log in to the database and view table names.
   -  When the query permission on a database is added to or deleted from a role, the query permission on tables in the database is automatically added to or deleted from the role.

Concepts
--------

.. table:: **Table 1** Scenarios of using Hive tables, columns, or databases

   ========================== ===================================
   Scenario                   Required Permission
   ========================== ===================================
   DESCRIBE TABLE             SELECT
   SHOW PARTITIONS            SELECT
   ANALYZE TABLE              SELECT and INSERT
   SHOW COLUMNS               SELECT
   SHOW TABLE STATUS          SELECT
   SHOW TABLE PROPERTIES      SELECT
   SELECT                     SELECT
   EXPLAIN                    SELECT
   CREATE VIEW                SELECT, Grant Of Select, and CREATE
   SHOW CREATE TABLE          SELECT and Grant Of Select
   CREATE TABLE               CREATE
   ALTER TABLE ADD PARTITION  INSERT
   INSERT                     INSERT
   INSERT OVERWRITE           INSERT and DELETE
   LOAD                       INSERT and DELETE
   ALTER TABLE DROP PARTITION DELETE
   CREATE FUNCTION            Hive Admin Privilege
   DROP FUNCTION              Hive Admin Privilege
   ALTER DATABASE             Hive Admin Privilege
   ========================== ===================================
