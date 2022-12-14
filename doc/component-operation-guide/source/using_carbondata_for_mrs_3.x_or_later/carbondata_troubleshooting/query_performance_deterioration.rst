:original_name: mrs_01_1456.html

.. _mrs_01_1456:

Query Performance Deterioration
===============================

Symptom
-------

The query performance fluctuates when the query is executed in different query periods.

Possible Causes
---------------

During data loading, the memory configured for each executor program instance may be insufficient, resulting in more Java GCs. When GC occurs, the query performance deteriorates.

Troubleshooting Method
----------------------

On the Spark UI, the GC time of some executors is obviously higher than that of other executors, or all executors have high GC time.

Procedure
---------

Log in to Manager and choose **Cluster** > **Services** > **Spark2x**. On the displayed page, click the **Configurations** tab and then **All Configurations**, search for **spark.executor.memory** in the search box, and set its value to a larger value.

|image1|

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001349170105.png
