:original_name: mrs_01_1458.html

.. _mrs_01_1458:

Why Is Incorrect Output Displayed When I Perform Query with Filter on Decimal Data Type Values?
===============================================================================================

Question
--------

Why is incorrect output displayed when I perform query with filter on decimal data type values?

For example:

**select \* from carbon_table where num = 1234567890123456.22;**

Output:

.. code-block::

   +------+---------------------+--+
   | name |        num          |
   +------+---------------------+--+
   | IAA  | 1234567890123456.22 |
   | IAA  | 1234567890123456.21 |
   +------+---------------------+--+

Answer
------

To obtain accurate output, append BD to the number.

For example:

**select \* from carbon_table where num = 1234567890123456.22BD;**

Output:

.. code-block::

   +------+---------------------+--+
   | name |        num          |
   +------+---------------------+--+
   | IAA  | 1234567890123456.22 |
   +------+---------------------+--+
