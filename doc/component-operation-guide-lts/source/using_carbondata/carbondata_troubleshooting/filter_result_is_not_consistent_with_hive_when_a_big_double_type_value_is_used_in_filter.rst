:original_name: mrs_01_1455.html

.. _mrs_01_1455:

Filter Result Is not Consistent with Hive when a Big Double Type Value Is Used in Filter
========================================================================================

Symptom
-------

When double data type values with higher precision are used in filters, incorrect values are returned by filtering results.

Possible Causes
---------------

When double data type values with higher precision are used in filters, values are rounded off before comparison. Therefore, values of double data type with different fraction part are considered same.

Troubleshooting Method
----------------------

NA.

Procedure
---------

To avoid this problem, use decimal data type when high precision data comparisons are required, such as financial applications, equality and inequality checks, and rounding operations.

Reference Information
---------------------

NA.
