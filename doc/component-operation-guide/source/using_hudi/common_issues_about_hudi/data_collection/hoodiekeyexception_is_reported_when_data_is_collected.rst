:original_name: mrs_01_24079.html

.. _mrs_01_24079:

HoodieKeyException Is Reported When Data Is Collected
=====================================================

Question
--------

Is it possible to use a nullable field that contains null records as a primary key when creating a Hudi table?

Answer
------

No. HoodieKeyException will be thrown.

.. code-block::

   Caused by: org.apache.hudi.exception.HoodieKeyException: recordKey value: "null" for field: "name" cannot be null or empty.
   at org.apache.hudi.keygen.SimpleKeyGenerator.getKey(SimpleKeyGenerator.java:58)
   at org.apache.hudi.HoodieSparkSqlWriter$$anonfun$1.apply(HoodieSparkSqlWriter.scala:104)
   at org.apache.hudi.HoodieSparkSqlWriter$$anonfun$1.apply(HoodieSparkSqlWriter.scala:100)
