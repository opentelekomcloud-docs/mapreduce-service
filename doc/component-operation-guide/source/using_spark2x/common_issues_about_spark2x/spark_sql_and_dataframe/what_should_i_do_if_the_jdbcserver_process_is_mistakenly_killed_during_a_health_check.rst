:original_name: mrs_01_2038.html

.. _mrs_01_2038:

What Should I Do If the JDBCServer Process is Mistakenly Killed During a Health Check?
======================================================================================

Question
--------

During a health check, if the concurrent statements exceed the threshold of the thread pool, the health check statements fail to be executed, the health check program times out, and the Spark JDBCServer process is killed.

Answer
------

There are two thread poolsHiveServer2-Handler-Pool and HiveServer2-Background-Pool in the current JDBCServer. The HiveServer2-Handler-Pool is used to connect sessions and the HiveServer2-Background-Pool is used to run Spark SQL statements.

The current health check mechanism establishes a session connection and runs the health check command **HEALTHCHECK** in the thread of the session to check the health condition of the Spark JDBCServer. Therefore, one thread must be reserved for the HiveServer2-Handler-Pool respectively to connect sessions and run statements for the health check. Otherwise, the session connection and statement running will fail and the Spark JDBCServer will be killed because it is mistakenly considered unhealthy. For example, if there are 100 threads in the HiveServer2-Handler-Pool respectively, a maximum of 99 sessions can be connected.
