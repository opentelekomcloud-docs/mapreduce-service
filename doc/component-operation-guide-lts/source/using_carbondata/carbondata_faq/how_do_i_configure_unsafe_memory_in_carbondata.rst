:original_name: mrs_01_1472.html

.. _mrs_01_1472:

How Do I Configure Unsafe Memory in CarbonData?
===============================================

Question
--------

How do I configure unsafe memory in CarbonData?

Answer
------

In the Spark configuration, the value of **spark.yarn.executor.memoryOverhead** must be greater than the sum of (**sort.inmemory.size.inmb** + **Netty offheapmemory required**), or the sum of (**carbon.unsafe.working.memory.in.mb** + **carbon.sort.inememory.storage.size.in.mb** + **Netty offheapmemory required**). Otherwise, if off-heap access exceeds the configured executor memory, Yarn may stop the executor.

If **spark.shuffle.io.preferDirectBufs** is set to **true**, the netty transfer service in Spark takes off some heap memory (around 384 MB or 0.1 x executor memory) from **spark.yarn.executor.memoryOverhead**.

For details, see :ref:`Configuring Executor Off-Heap Memory <mrs_01_1947>`.
