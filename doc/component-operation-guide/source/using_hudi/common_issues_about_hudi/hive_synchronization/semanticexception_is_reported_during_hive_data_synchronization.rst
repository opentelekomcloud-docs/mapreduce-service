:original_name: mrs_01_24083.html

.. _mrs_01_24083:

SemanticException Is Reported During Hive Data Synchronization
==============================================================

Question
--------

The following error is reported during Hive data synchronization:

.. code-block::

   org.apache.hadoop.hive.ql.parse.SemanticException: Database does not exist: test_db

Answer
------

This error usually occurs when Hive synchronization is performed on the Hudi dataset but the configured **hive_sync** database does not exist.

Create the corresponding database on your Hive cluster and try again.
