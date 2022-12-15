:original_name: mrs_01_2033.html

.. _mrs_01_2033:

Why the Operation Fails When the Table Name Is TABLE?
=====================================================

Question
--------

When the table name is set to **table**, why the error information similar to the following is displayed after the **drop table table** command or other command is run?

.. code-block::

   16/07/12 18:56:29 ERROR SparkSQLDriver: Failed in [drop table table]
   java.lang.RuntimeException: [1.1] failure: identifier expected
   table
   ^
   at scala.sys.package$.error(package.scala:27)
   at org.apache.spark.sql.catalyst.SqlParserTrait$class.parseTableIdentifier(SqlParser.scala:56)
   at org.apache.spark.sql.catalyst.SqlParser$.parseTableIdentifier(SqlParser.scala:485)

Answer
------

The word table is a keyword of Spark SQL statements and must not be used as a table name.
