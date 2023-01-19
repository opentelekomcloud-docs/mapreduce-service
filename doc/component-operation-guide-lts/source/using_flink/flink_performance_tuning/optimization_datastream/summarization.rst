:original_name: mrs_01_1593.html

.. _mrs_01_1593:

Summarization
=============

Avoiding Data Skew
------------------

If data skew occurs (certain data volume is large), the execution time of tasks is inconsistent even if no garbage collection is performed.

-  Redefine keys. Use keys of smaller granularity to optimize the task size.
-  Modify the DOP.
-  Call the rebalance operation to balance data partitions.

Setting Timeout Interval for the Buffer
---------------------------------------

-  During the execution of tasks, data is switched through network switching. You can configure the **setBufferTimeout** parameter to specify the timeout interval for the buffer.

-  If **setBufferTimeout** is set to **-1**, the refreshing operation is performed when the buffer full, maximizing the throughput. If **setBufferTimeout** is set to **0**, the refreshing operation is performed each time data is received, minimizing the delay. If **setBufferTimeout** is set to a value greater than **0**, the refreshing operation is performed after the butter times out.

   The following is an example:

   .. code-block::

      env.setBufferTimeout(timeoutMillis);

      env.generateSequence(1,10).map(new MyMapper()).setBufferTimeout(timeoutMillis);
