:original_name: mrs_01_24504.html

.. _mrs_01_24504:

Hudi Fails to Write Decimal Data with Lower Precision
=====================================================

Question
--------

Decimal data is initially written to a Hudi table using the **BULK_INSERT** command. Then when data is subsequently written using **UPSERT**, the following error is reported:

.. code-block::

   java.lang.UnsupportedOperationException: org.apache.parquet.avro.AvroConverters$FieldFixedConverter

Answer
------

**Cause:**

The Hudi table contains decimal data.

The initial bulk insert of data is implemented using the Spark class for writing Parquet files. However, Spark processes the decimal data with different precisions differently.

When data is written using the **UPSERT** command, Hudi uses the Avro-compliant class for writing Parquet files, which is incompatible with the Spark class.

**Solutions:**

When executing the **BULK_INSERT** command, set **hoodie.datasource.write.row.writer.enable** to **false** to enable Hoodie to use the Avro-compliant class for writing Parquet files.
