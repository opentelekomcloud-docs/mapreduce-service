:original_name: mrs_01_2029.html

.. _mrs_01_2029:

How to Use Cache Table?
=======================

Question
--------

What is cache table used for? Which point should I pay attention to while using cache table?

Answer
------

Spark SQL caches tables into memory so that data can be directly read from memory instead of disks, reducing memory overhead due to disk reads.

Note that cached tables consume Executor's memory. This means that caching large or many tables compromises Executor's stability even if compressed storage has been used to reduce memory overhead as much as possible.

If it is no longer necessary to accelerate data query by means of cache table, run the following command to uncache tables to free up memory:

**uncache table** *table_name*

.. note::

   The Storage tab page of the Spark Driver user interface displays the cached tables.
