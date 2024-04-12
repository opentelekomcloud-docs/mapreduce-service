:original_name: mrs_01_2352.html

.. _mrs_01_2352:

Configuring Permissions for Tables, Columns, and Databases
==========================================================

If a user needs to access HetuEngine tables or databases created by other users, the user needs to be granted with related permissions. HetuEngine supports permission control based on columns for strict permission control. If a user needs to access some columns in tables created by other users, the user must be granted the permission for columns. The following describes how to grant table, column, and database permissions to users by using the role management function of Manager.

Procedure
---------

The operations for granting permissions on HetuEngine tables, columns, and databases are the same as those for Hive.

.. note::

   -  Any permission for a table in the database is automatically associated with the HDFS permission for the database directory to facilitate permission management. When any permission for a table is canceled, the system does not automatically cancel the HDFS permission for the database directory to ensure performance. In this case, users can only log in to the database and view table names.
   -  When the query permission on a database is added to or deleted from a role, the query permission on tables in the database is automatically added to or deleted from the role. This mechanism is inherited from Hive.
   -  In HetuEngine, the name of a column of the **struct** type data cannot contain special characters, that is, characters other than letters, digits, and underscores (_). If the column name of the struct data type contains special characters, the column cannot be displayed on the FusionInsight Manager console when you grant permissions to roles on the **Role** page.

Concepts
--------

:ref:`Table 1 <mrs_01_2352__en-us_topic_0000001173789716_t61b1f27ae37c4015ac2596a8c29aa39e>` describes the permission requirements when SQL statements are processed in HetuEngine.

.. _mrs_01_2352__en-us_topic_0000001173789716_t61b1f27ae37c4015ac2596a8c29aa39e:

.. table:: **Table 1** Using HetuEngine tables, columns, or data

   +----------------------------+-------------------------------------------------------------------------------------------+
   | Scenario                   | Required Permission                                                                       |
   +============================+===========================================================================================+
   | DESCRIBE TABLE             | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | ANALYZE TABLE              | Select and Insert                                                                         |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | SHOW COLUMNS               | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | SHOW TABLE STATUS          | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | SHOW TABLE PROPERTIES      | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | SELECT                     | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | EXPLAIN                    | Select                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | CREATE VIEW                | Select, Grant Of Select, and Create                                                       |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | CREATE TABLE               | Create                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | ALTER TABLE ADD PARTITION  | Insert                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | INSERT                     | Insert                                                                                    |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | INSERT OVERWRITE           | Insert and Delete                                                                         |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | ALTER TABLE DROP PARTITION | The table-level Alter and Delete, and column-level Select permissions need to be granted. |
   +----------------------------+-------------------------------------------------------------------------------------------+
   | ALTER DATABASE             | Hive Admin Privilege                                                                      |
   +----------------------------+-------------------------------------------------------------------------------------------+
