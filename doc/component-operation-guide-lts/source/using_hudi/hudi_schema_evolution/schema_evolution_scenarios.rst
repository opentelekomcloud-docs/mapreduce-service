:original_name: mrs_01_24494.html

.. _mrs_01_24494:

Schema Evolution Scenarios
==========================

Schema evolution scenarios

-  Columns (including nested columns) can be added, deleted, modified, and moved.
-  Partition columns cannot be evolved.
-  You cannot add, delete, or perform operations on nested columns of the Array type.

.. table:: **Table 1** Engines supported

   +------------+---------------+----------------------------+---------------------------+---------------------------------+
   | Component  | DDL Operation | Hudi Table Write Operation | Hudi Table Read Operation | Hudi Table Compaction Operation |
   +============+===============+============================+===========================+=================================+
   | SparkSQL   | Y             | Y                          | Y                         | Y                               |
   +------------+---------------+----------------------------+---------------------------+---------------------------------+
   | Flink      | N             | Y                          | Y                         | Y                               |
   +------------+---------------+----------------------------+---------------------------+---------------------------------+
   | HetuEngine | N             | N                          | Y                         | N                               |
   +------------+---------------+----------------------------+---------------------------+---------------------------------+
   | Hive       | N             | N                          | Y                         | N                               |
   +------------+---------------+----------------------------+---------------------------+---------------------------------+
