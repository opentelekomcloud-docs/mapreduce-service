:original_name: mrs_01_24037.html

.. _mrs_01_24037:

Read
====

The read operation of Hudi applies to three views of Hudi. You can select a proper view for query based on requirements.

Hudi supports multiple query engines, including Spark and Hive. For details, see :ref:`Table 1 <mrs_01_24037__table42155834714>` and :ref:`Table 2 <mrs_01_24037__table8194141519510>`.

.. _mrs_01_24037__table42155834714:

.. table:: **Table 1** COW tables

   +-----------------------------+------------------------------------+------------------+
   | Query Engine                | Real-time View/Read-optimized View | Incremental View |
   +=============================+====================================+==================+
   | Hive                        | Y                                  | Y                |
   +-----------------------------+------------------------------------+------------------+
   | Spark (SparkSQL)            | Y                                  | Y                |
   +-----------------------------+------------------------------------+------------------+
   | Spark (SparkDataSource API) | Y                                  | Y                |
   +-----------------------------+------------------------------------+------------------+

.. _mrs_01_24037__table8194141519510:

.. table:: **Table 2** MOR tables

   +-----------------------------+----------------+------------------+---------------------+
   | Query Engine                | Real-time View | Incremental View | Read-optimized View |
   +=============================+================+==================+=====================+
   | Hive                        | Y              | Y                | Y                   |
   +-----------------------------+----------------+------------------+---------------------+
   | Spark (SparkSQL)            | Y              | Y                | Y                   |
   +-----------------------------+----------------+------------------+---------------------+
   | Spark (SparkDataSource API) | Y              | Y                | Y                   |
   +-----------------------------+----------------+------------------+---------------------+

.. caution::

   -  Currently, the partition deduction capability is not supported when Hudi uses the Spark DataSource API to read data. For example, when the DataSource API is used to query a bootstrap table, the partition field may not be displayed or may be displayed as null.
   -  For an incremental view, set **hoodie.hudicow.consume.mode** to **INCREMENTAL**. This parameter applies only to queries on the incremental view and cannot be used for queries on other types of Hudi tables or queries on other tables. You can set **hoodie.hudicow.consume.mode** to **SNAPSHOT** or any value to restore the configuration.

-  :ref:`Reading COW Table Views <mrs_01_24098>`
-  :ref:`Reading MOR Table Views <mrs_01_24099>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   reading_cow_table_views
   reading_mor_table_views
