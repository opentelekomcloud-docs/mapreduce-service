:original_name: mrs_01_24078.html

.. _mrs_01_24078:

HoodieException Is Reported When Data Is Collected
==================================================

Question
--------

The following error is reported when data is collected:

.. code-block::

   com.uber.hoodie.exception.HoodieException: created_at(Part -created_at) field not found in record. Acceptable fields were :[col1, col2, col3, id, name, dob, created_at, updated_at]

Answer
------

This error usually occurs when a field marked as recordKey or partitionKey is not present in the input record. Cross verify the input record.
