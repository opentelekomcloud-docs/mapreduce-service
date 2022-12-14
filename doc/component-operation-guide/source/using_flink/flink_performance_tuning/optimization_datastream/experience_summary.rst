:original_name: mrs_01_1593.html

.. _mrs_01_1593:

Experience Summary
==================

Avoiding Data Skew
------------------

If data skew occurs (certain data volume is extremely large), the execution time of tasks is inconsistent even though no GC is performed.

-  Redefine keys. Use keys of smaller granularity to optimize the task size.
-  Modify the DOP.
-  Call the rebalance operation to balance data partitions.

Setting Timeout Interval for the Buffer
---------------------------------------

-  During the execution of tasks, data is exchanged through network. You can set the **setBufferTimeout** parameter to specify a buffer timeout interval for data exchanging among different servers.

-  If **setBufferTimeout** is set to **-1**, the refreshing operation is performed when the buffer is full to maximize the throughput. If **setBufferTimeout** is set to **0**, the refreshing operation is performed each time data is received to minimize the delay. If **setBufferTimeout** is set to a value greater than **0**, the refreshing operation is performed after the buffer times out.

   The following is an example:

   .. code-block::

      env.setBufferTimeout(timeoutMillis);

      env.generateSequence(1,10).map(new MyMapper()).setBufferTimeout(timeoutMillis);
