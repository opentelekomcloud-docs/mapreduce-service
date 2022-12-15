:original_name: mrs_01_2310.html

.. _mrs_01_2310:

Why Does Hive Not Support Concurrent Data Writing to the Same Table or Partition?
=================================================================================

Question
--------

Why Does Data Inconsistency Occur When Data Is Concurrently Written to a Hive Table Through an API?

Answer
------

Hive does not support concurrent data insertion for the same table or partition. As a result, multiple tasks perform operations on the same temporary data directory, and one task moves the data of another task, causing task data exception. The service logic is modified so that data is inserted to the same table or partition in single thread mode.
