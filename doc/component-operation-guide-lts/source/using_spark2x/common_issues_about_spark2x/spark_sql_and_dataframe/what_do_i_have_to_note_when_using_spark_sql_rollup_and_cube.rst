:original_name: mrs_01_2023.html

.. _mrs_01_2023:

What Do I have to Note When Using Spark SQL ROLLUP and CUBE?
============================================================

Question
--------

Suppose that there is a table src(d1, d2, m) with the following data:

.. code-block::

   1 a 1
   1 b 1
   2 b 2

The results for statement "select d1, sum(d1) from src group by d1, d2 with rollup" are shown as below:

.. code-block::

   NULL 0
   1    2
   2    2
   1    1
   1    1
   2    2

Why the first line of the above results is (NULL,0), rather than (NULL,4)?

Answer
------

When conducting the rollup and cube operation, we usually perform the dimension-based analysis and what we need is the measurement result, so we would not conduct aggregation operation on the dimension.

Suppose that there is a table src(d1, d2, m), so the statement 1 "select d1, sum(m) from src group by d1, d2 with rollup" conducts the rollup operation on the dimension d1 and d2 to compute the result of m. It has actual business meaning, and its results are in line with the expectation. However, the statement 2 "select d1, sum(d1) from src group by d1, d2 with rollup" cannot be explained from the business perspective. For the statement 2, the result for all aggregations (sum/avg/max/min) is 0.

.. note::

   Only when there is an aggregation operation for fields in "group by" in the rollup and cube operation, the result is 0. For non-rollup and non-cube operations, the result will be in line with the expectation.
