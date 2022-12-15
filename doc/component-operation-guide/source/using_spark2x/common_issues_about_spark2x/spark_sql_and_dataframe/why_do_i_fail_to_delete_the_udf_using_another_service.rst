:original_name: mrs_01_2027.html

.. _mrs_01_2027:

Why Do I Fail to Delete the UDF Using Another Service?
======================================================

Question
--------

Why do I fail to delete the UDF using another service, for example, delete the UDF created by Hive using Spark SQL.

Answer
------

The UDF can be created using any of the following services:

#. Hive client.
#. JDBCServer API. You can connect JDBCServer to Spark Beeline or JDBC client code, and run SQL statements to create the UDF.
#. spark-sql.

The scenarios in which the UDF failed to be deleted may be as follows:

-  If you use Spark Beeline to delete the UDF created by other services, you must restart the JDBCServer before the deletion. Otherwise, the deletion fails. If you use spark-sql to delete the UDF created by other services, you must restart the spark-sql before the deletion. Otherwise, the deletion fails.

   Cause: After the UDF is created, if the JDBCServer or the spark-sql has not been restarted, the newly created UDF will not be saved by the FunctionRegistry object in the thread where Spark locates. As a result, the UDF failed to be deleted.

   Solution: Restart the JDBCServer and spark-sql of the Spark client and delete the UDF.

-  When creating UDF on the Hive client, the **add jar** command (e.g. **add jar /opt/test/two_udfs.jar**) is used to add the **.jar** package instead of specifying the path of **.jar** package in creating UDF statement. As a result, the **ClassNotfound** error occurs when you use other services to delete the UDF.

   Cause: When you use a service to delete the UDF, the service will load the class that corresponds to the UDF to obtain the UDF. However, the **.jar** package is added by the **add jar** command and jar package does not exist in the classpath of other services. As a result, the **ClassNotfound** error occurs and the UDF failed to be deleted.

   Solution: The UDF created using the preceding approach must be deleted using the same approach. No other approaches are allowed.
