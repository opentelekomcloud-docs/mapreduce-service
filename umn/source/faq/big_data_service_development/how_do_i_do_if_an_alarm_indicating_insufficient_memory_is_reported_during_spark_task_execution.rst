:original_name: mrs_03_1206.html

.. _mrs_03_1206:

How Do I Do If an Alarm Indicating Insufficient Memory Is Reported During Spark Task Execution?
===============================================================================================

Symptom
-------

When a Spark task is executed, an alarm indicating insufficient memory is reported. The alarm ID is 18022. As a result, no available memory can be used.

Procedure
---------

Set the executor parameters in the SQL script to limit the number of cores and memory of an executor.

For example, the configuration is as follows:

.. code-block::

   set hive.execution.engine=spark;
   set spark.executor.cores=2;
   set spark.executor.memory=4G;
   set spark.executor.instances=10;

Change the values of the parameters as required.
