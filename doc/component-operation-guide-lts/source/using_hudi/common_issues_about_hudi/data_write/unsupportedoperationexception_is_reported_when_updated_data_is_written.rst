:original_name: mrs_01_24072.html

.. _mrs_01_24072:

UnsupportedOperationException Is Reported When Updated Data Is Written
======================================================================

Question
--------

The following error is reported when data is written:

.. code-block::

   java.lang.UnsupportedOperationException: org.apache.parquet.avro.AvroConverters$FieldIntegerConverter

Answer
------

This error will occur again because schema evolutions are in non-backwards compatible mode. Basically, there is some update U for a record R which is already written to the Hudi dataset in the Parquet file. R contains field F which includes certain data type, that is long. U has the same field F with the int data type. Parquet FS does not support incompatible data type conversions.

For such errors, perform valid data type conversions in the data source where you collect data.
