:original_name: mrs_01_2054.html

.. _mrs_01_2054:

Why Is the Input Size Corresponding to Batch Time on the Web UI Set to 0 Records When Kafka Is Restarted During Spark Streaming Running?
========================================================================================================================================

Question
--------

When the Kafka is restarted during the execution of the Spark Streaming application, the application cannot obtain the topic offset from the Kafka. As a result, the job fails to be generated. As shown in :ref:`Figure 1 <mrs_01_2054__f4c352ef623b7496485289010f2d69e3c>`, **2017/05/11 10:57:00-2017/05/11 10:58:00** indicates the Kafka restart time. After the restart is successful at 10:58:00 on May,11,2017, the value of **Input Size** is **0 records**.

.. _mrs_01_2054__f4c352ef623b7496485289010f2d69e3c:

.. figure:: /_static/images/en-us_image_0000001349090029.png
   :alt: **Figure 1** On the Web UI, the **input size** corresponding to the **batch time** is **0 records**.

   **Figure 1** On the Web UI, the **input size** corresponding to the **batch time** is **0 records**.

Answer
------

After Kafka is restarted, the application supplements the missing RDD between 10:57:00 on May 11, 2017 and 10:58:00 on May 11, 2017 based on the batch time. Although the number of read data records displayed on the UI is **0**, the missing data is processed in the supplemented RDD. Therefore, no data loss occurs.

The data processing mechanism during the Kafka restart period is as follows:

The Spark Streaming application uses the **state** function (for example, **updateStateByKey**). After Kafka is restarted, the Spark Streaming application generates a batch task at 10:58:00 on May 11, 2017. The missing RDD between10:57:00 on May 11, 2017 and 10:58:00 on May 11, 2017 is supplemented based on the batch time (data that is not read in Kafka before Kafka restart, which belongs to the batch before 10:57:00 on May 11, 2017).
