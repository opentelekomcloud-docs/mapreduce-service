:original_name: mrs_01_2350.html

.. _mrs_01_2350:

Creating a HetuEngine Role
==========================

The system administrator can create and set a HetuEngine role on FusionInsight Manager. The HetuEngine role can be configured with the HetuEngine administrator permission or the permission of performing operations on the table data.

Creating a database with Hive requires users to join in the Hive group, without granting a role. Users have all permissions on the databases or tables created by themselves in Hive or HDFS. They can create tables, select, delete, insert, or update data, and grant permissions to other users to allow them to access the tables and corresponding HDFS directories and files. The created databases or tables are saved in the **/user/hive/warehouse** directory of HDFS by default.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **System** > **Permission** > **Role**.

#. Click **Create Role**, and set **Role Name** and **Description**.

#. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > **Hive** and set role permissions. For details, see :ref:`Table 1 <mrs_01_2350__en-us_topic_0000001173631158_en-us_topic_0254454613_table1148121718119>`.

   -  **Hive Admin Privilege**: Hive administrator permission.
   -  **Hive Read Write Privileges**: Hive data table management permission, which is the operation permission to set and manage the data of created tables.

   .. note::

      -  Hive role management supports the Hive administrator permission, and the permissions of accessing tables and views, without granting the database permission.
      -  The permissions of the Hive administrator do not include the permission to manage HDFS.
      -  If there are too many tables in the database or too many files in tables, the permission granting may last a while. For example, if a table contains 10,000 files, the permission granting lasts about 2 minutes.

   .. _mrs_01_2350__en-us_topic_0000001173631158_en-us_topic_0254454613_table1148121718119:

   .. table:: **Table 1** Setting a role

      +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
      | Scenario                                                                                 | Role Authorization                                                                                      |
      +==========================================================================================+=========================================================================================================+
      | Setting the permission to query a table of another user in the default database          | a. In the **View Name** area, click **Hive Read Write Privileges**.                                     |
      |                                                                                          | b. Click the name of the specified database in the database list. Tables in the database are displayed. |
      |                                                                                          | c. In the **Permission** column of a specified table, choose **Select**.                                |
      +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
      | Setting the permission to import data to a table of another user in the default database | a. In the **View Name** area, click **Hive Read Write Privileges**.                                     |
      |                                                                                          | b. Click the name of the specified database in the database list. Tables in the database are displayed. |
      |                                                                                          | c. In the **Permission** column of the specified indexes, select **Delete** and **Insert**.             |
      +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

5. Click **OK**. Return to the **Role** page.
