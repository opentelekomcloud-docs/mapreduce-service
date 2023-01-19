:original_name: mrs_01_24082.html

.. _mrs_01_24082:

HoodieHiveSyncException Is Reported During Hive Data Synchronization
====================================================================

Question
--------

The following error is reported during Hive data synchronization:

.. code-block::

   com.uber.hoodie.hive.HoodieHiveSyncException: Could not convert field Type from <type1> to <type2> for field col1

Answer
------

This error occurs because HiveSyncTool currently supports only few compatible data type conversions. The exception is thrown if any other incompatible changes are made.

Check the data type evolution for the related field and verify if it indeed can be considered as a valid data type conversion based on the Hudi code base.
