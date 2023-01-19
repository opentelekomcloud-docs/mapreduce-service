:original_name: mrs_01_1790.html

.. _mrs_01_1790:

Why Does a MapReduce Task Stay Unchanged for a Long Time?
=========================================================

Question
--------

MapReduce job is not progressing for long time

Answer
------

This is because of less memory. When the memory is less, the time taken by the job to copy the map output increases significantly.

In order to reduce the waiting time, increase the heap memory.

The job configuration should be tuned according to number of mappers and data size processed by each mapper. Based on the input data size, tune the following configurations accordingly for feasible performance.

-  **mapreduce.reduce.memory.mb**
-  **mapreduce.reduce.java.opts**

**Example**: If the data size is 5 GB with 10 mappers, then the ideal heap memory would be 1.5 GB. Increase the heap memory size according with the increase in data size.
