:original_name: mrs_01_2055.html

.. _mrs_01_2055:

Why the Job Information Obtained from the restful Interface of an Ended Spark Application Is Incorrect?
=======================================================================================================

Question
--------

The job information obtained from the restful interface of an ended Spark application is incorrect: the value of **numActiveTasks** is negative, as shown in :ref:`Figure 1 <mrs_01_2055__en-us_topic_0000001219230555_f25d2e3813ec3476b9a49627d17776421>`:

.. _mrs_01_2055__en-us_topic_0000001219230555_f25d2e3813ec3476b9a49627d17776421:

.. figure:: /_static/images/en-us_image_0000001296060112.png
   :alt: **Figure 1** job information

   **Figure 1** job information

.. note::

   numActiveTasks indicates the number of active tasks.

Answer
------

The job information can be obtained in either of the following methods:

-  Set **spark.history.briefInfo.gather=true** and then view the brief JobHistory information.
-  Visit the JobHistory2x page of Spark (URL: https://IP:port/api/v1/<appid>/jobs/).

The value of **numActiveTasks** in the job information is calculated from the difference between the number of SparkListenerTaskStart events and the number of SparkListenerTaskEnd events in the **eventLog** file. If some events are not recorded in the **eventLog** file, the job information obtained from the restful interface is incorrect.
