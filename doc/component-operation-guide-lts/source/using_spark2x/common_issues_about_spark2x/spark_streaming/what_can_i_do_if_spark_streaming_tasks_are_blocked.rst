:original_name: mrs_01_2050.html

.. _mrs_01_2050:

What Can I Do If Spark Streaming Tasks Are Blocked?
===================================================

Question
--------

After a Spark Streaming task is run and data is input, no processing result is displayed. Open the web page to view the Spark job execution status. The following figure shows that two jobs are waiting to be executed but cannot be executed successfully.

.. _mrs_01_2050__en-us_topic_0000001219149015_f4bfff9246c4744c5b796657f0834fa67:

.. figure:: /_static/images/en-us_image_0000001295739868.jpg
   :alt: **Figure 1** Active Jobs

   **Figure 1** Active Jobs

Check the completed jobs. Only two jobs are found, indicating that Spark Streaming does not trigger data computing tasks. (By default, Spark Streaming has two jobs that attempt to run. See the figure below.)


.. figure:: /_static/images/en-us_image_0000001349258973.jpg
   :alt: **Figure 2** Completed Jobs

   **Figure 2** Completed Jobs

Answer
------

After fault locating, it is found that the number of computing cores of Spark Streaming is less than the number of receivers. As a result, after some receivers are started, no resource is available to run computing tasks. Therefore, the first task keeps waiting and subsequent tasks keep queuing. :ref:`Figure 1 <mrs_01_2050__en-us_topic_0000001219149015_f4bfff9246c4744c5b796657f0834fa67>` is an example of two queuing tasks.

To address this problem, it is advised to check whether the number of Spark cores is greater than the number of receivers when two tasks are queuing.

.. note::

   Receiver is a permanent Spark job in Spark Streaming. It is common for Spark, but its life cycle is the same as that of a Spark Streaming task and occupies one computing core.

   Pay attention to the relationship between the number of cores and the number of receivers in scenarios where default configurations are often used, such as debugging and testing.
