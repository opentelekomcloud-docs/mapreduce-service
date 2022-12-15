:original_name: mrs_03_1248.html

.. _mrs_03_1248:

It Takes a Long Time for Spark SQL to Access Hive Partitioned Tables Before Job Startup
=======================================================================================

Symptom
-------

When Spark SQL is used to access Hive partitioned tables stored in OBS, the acces speed is slow and a large number of OBS query APIs are called.

Example SQL:

.. code-block::

   select a,b,c from test where b=xxx

Fault Locating
--------------

According to the configuration, the task should scan only the partition whose b is *xxx*. However, the task logs show that the task scans all partitions and then calculates the data whose b is *xxx*. As a result, the task calculation is slow. In addition, a large number of OBS requests are sent because all files need to be scanned.

By default, the execution plan optimization based on partition statistics is enabled on MRS, which is equivalent to automatic execution of Analyze Table. (The default configuration method is to set **spark.sql.statistics.fallBackToHdfs** to **true**. You can set this parameter to **false**.) After this function is enabled, table partition statistics are scanned during SQL execution and used as cost estimation in the execution plan. For example, small tables identified during cost evaluation are broadcast to each node in the memory for join operations, significantly reducing shuffle time. This function greatly optimizes performance in join scenarios, but increases the number of OBS calls.

Procedure
---------

Set the following parameter in Spark SQL and then run the SQL statement:

.. code-block::

   set spark.sql.statistics.fallBackToHdfs=false;

Alternatively, run the **--conf** command to set this parameter to **false** before startup.

.. code-block::

   --conf spark.sql.statistics.fallBackToHdfs=false
