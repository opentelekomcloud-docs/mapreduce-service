:original_name: mrs_01_1422.html

.. _mrs_01_1422:

CarbonData Access Control
=========================

The following table provides details about Hive ACL permissions required for performing operations on CarbonData tables.

Prerequisites
-------------

Parameters listed in :ref:`Table 5 <mrs_01_1404__en-us_topic_0000001219350555_ta902cd071dfb426097416a5c7034ee6c>` or :ref:`Table 6 <mrs_01_1404__en-us_topic_0000001219350555_t3897ae14f205433fb0f98b79411cfa0c>` have been configured.

Hive ACL permissions
--------------------

.. table:: **Table 1** Hive ACL permissions required for CarbonData table-level operations

   +--------------------------------------+---------------------------------------------------------------------------------+
   | Scenario                             | Required Permission                                                             |
   +======================================+=================================================================================+
   | DESCRIBE TABLE                       | SELECT (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | SELECT                               | SELECT (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | EXPLAIN                              | SELECT (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | CREATE TABLE                         | CREATE (of database)                                                            |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | CREATE TABLE As SELECT               | CREATE (on database), INSERT (on table), RW on data file, and SELECT (on table) |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | LOAD                                 | INSERT (of table) RW on data file                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | DROP TABLE                           | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | DELETE SEGMENTS                      | DELETE (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | SHOW SEGMENTS                        | SELECT (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | CLEAN FILES                          | DELETE (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | INSERT OVERWRITE / INSERT INTO       | INSERT (of table) RW on data file and SELECT (of table)                         |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | CREATE INDEX                         | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | DROP INDEX                           | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | SHOW INDEXES                         | SELECT (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE ADD COLUMN               | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE DROP COLUMN              | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE CHANGE DATATYPE          | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE RENAME                   | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE COMPACTION               | INSERT (on table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | FINISH STREAMING                     | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE SET STREAMING PROPERTIES | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE SET TABLE PROPERTIES     | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | UPDATE CARBON TABLE                  | UPDATE (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | DELETE RECORDS                       | DELETE (of table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | REFRESH TABLE                        | OWNER (of main table)                                                           |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | REGISTER INDEX TABLE                 | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | SHOW PARTITIONS                      | SELECT (on table)                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE ADD PARTITION            | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+
   | ALTER TABLE DROP PARTITION           | OWNER (of table)                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------+

.. note::

   -  If tables in the database are created by multiple users, the **Drop database** command fails to be executed even if the user who runs the command is the owner of the database.

   -  In a secondary index, when the parent table is triggered, **insert** and **compaction** are triggered on the index table. If you select a query that has a filter condition that matches index table columns, you should provide selection permissions for the parent table and index table.

   -  The LockFiles folder and lock files created in the LockFiles folder will have full permissions, as the LockFiles folder does not contain any sensitive data.

   -  If you are using ACL, ensure you do not configure any path for DDL or DML which is being used by other process. You are advised to create new paths.

      Configure the path for the following configuration items:

      1) carbon.badRecords.location

      2) Db_Path and other items during database creation

   -  For Carbon ACL in a non-security cluster, **hive.server2.enable.doAs** in the **hive-site.xml** file must be set to **false**. Then the query will run as the user who runs the hiveserver2 process.
