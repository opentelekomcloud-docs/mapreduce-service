:original_name: mrs_01_1468.html

.. _mrs_01_1468:

Why CarbonData tables created in V100R002C50RC1 not reflecting the privileges provided in Hive Privileges for non-owner?
========================================================================================================================

Question
--------

Why CarbonData tables created in V100R002C50RC1 not reflecting the privileges provided in Hive Privileges for non-owner?

Answer
------

The Hive ACL is implemented after the version V100R002C50RC1, hence the Hive ACL Privileges are not reflecting.

To support HIVE ACL Privileges for CarbonData tables created in V100R002C50RC1, following two ALTER TABLE commands must be executed by owner of the table.

**ALTER TABLE** *$dbname.$tablename SET LOCATION '$carbon.store/$dbname/$tablename';*

**ALTER TABLE** *$dbname.$tablename SET SERDEPROPERTIES ('path'='$carbon.store/$dbname/$tablename');*

Example:

Assume database name is 'carbondb', table name is 'carbontable', and CarbonData store location is 'hdfs://hacluster/user/hive/warehouse/carbon.store', then the commands should be executed is as follows:

**ALTER TABLE** *carbondb.carbontable SET LOCATION 'hdfs://hacluster/user/hive/warehouse/carbon.store/carbondb/carbontable';*

**ALTER TABLE** *carbondb.carbontable SET SERDEPROPERTIES ('path'='hdfs://hacluster/user/hive/warehouse/carbon.store/carbondb/carbontable');*
