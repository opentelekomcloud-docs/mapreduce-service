:original_name: mrs_01_24262.html

.. _mrs_01_24262:

Constraints
===========

Hudi 0.9.0 adds Spark SQL DDL and DML statements for using Hudi, making it easier for all users (including non-engineers or analysts) to access and operate Hudi.


Constraints
-----------

-  You can use Spark SQL to operate Hudi on the Hudi client.
-  You can use Spark SQL to operate Hudi in JDBCServer of Spark2x.
-  You cannot use Spark SQL to operate Hudi on the Spark2x client.
-  You cannot operate Hudi in the Hive or Hetu engine.
-  The default value of **KeyGenerator** in SQL is **org.apache.hudi.keygen.ComplexKeyGenerator**. Therefore, you need to set the **KeyGenerator** value to that of SQL when data is written in DataSource mode.
-  If you run the **Show Partitions** command for the first time, you need to run the **msck repair** command as prompted.
-  Spark SQL does not support incremental view query.
-  Spark SQL does not support ALTER CHANGE DATA TYPE.
-  To write data incrementally using SQL into a COW table created using DataSource, you need to run the **ALTER TABLE** *table_name* **SET SERDEPROPERTIES(primaryKey='**\ *xx*\ **',preCombineField='**\ *xx*\ **')** statement in SQL to reset two properties of the table. To write data incrementally using SQL into an MOR table created using DataSource, you need to specify a path to the one set for creating this MOR table.
