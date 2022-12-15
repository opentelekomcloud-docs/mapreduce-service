:original_name: mrs_03_1208.html

.. _mrs_03_1208:

Why DataArtsStudio Occasionally Fail to Schedule Spark Jobs and the Rescheduling also Fails?
============================================================================================

Symptom
-------

DataArtsStudio occasionally fails to schedule Spark jobs and the rescheduling also fails. The following error information is displayed:

.. code-block::

   Caused by: org.apache.spark.SparkException: Application application_1619511926396_2586346 finished with failed status

Solution
--------

Log in to the node where the Spark client is located as user **root** and increase the value of the **spark.driver.memory** parameter in the **spark-defaults.conf** file.
