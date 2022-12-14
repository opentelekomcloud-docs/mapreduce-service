:original_name: mrs_01_24073.html

.. _mrs_01_24073:

SchemaCompatabilityException Is Reported When Updated Data Is Written
=====================================================================

Question
--------

The following error is reported when data is written:

.. code-block::

   org.apache.hudi.exception.SchemaCompatabilityException: Unable to validate the rewritten record <record> against schema <schema>at org.apache.hudi.common.util.HoodieAvroUtils.rewrite(HoodieAvroUtils.java:215)

Answer
------

This error may occur if a schema contains some **non-nullable** field whose value is not present or is null.

You are advised to evolve schemas in backward compatible mode. Essentially, this means either you need to set each newly added field to null or to default values. In Hudi 0.5.1 and later versions, the troubleshooting is invalid if fields rely on default values.
