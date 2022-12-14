:original_name: mrs_01_1948.html

.. _mrs_01_1948:

Enhancing Stability in a Limited Memory Condition
=================================================

Scenario
--------

A large amount of memory is required when Spark SQL executes a query, especially during Aggregate and Join operations. If the memory is limited, OutOfMemoryError may occur. Stability in a limited memory condition ensures queries to be run in limited memory without OutOfMemoryError.

.. note::

   Limited memory does not mean infinitely small memory, but ensures stable queries by using disks in a scenario where memory fails to store the data amount that is several times larger than the available memory size. For example, for queries involving Join, the data of the same key used for Join needs to be stored in memory. If the data amount is too large to be stored in the available memory, OutOfMemoryError occurs.

Stability in a limited memory condition involves the following sub-functions:

#. ExternalSort

   If the memory is inadequate during sorting, partial data overflows to disks.

#. TungstenAggregate

   By default, ExternalSort is used to sort data before data aggregation. Therefore, if the memory is inadequate, the data overflows to disks during sorting. The data has been properly sorted before aggregation and only aggregation results of the current key are remained, which use a small amount of memory.

#. SortMergeJoin and SortMergeOuterJoin

   SortMergeJoin and SortMergeOuterJoinan are based on the equivalence join of sorted data. By default, ExternalSort is used to sort the data before the equivalence join. Therefore, if the memory is inadequate, the data overflows to disks during sorting. The data has been properly sorted before the equivalence join and only the data of the same key are remained, which uses a small amount of memory.

Configuration
-------------

**Navigation path for setting parameters:**

When submitting an application, set the following parameters using **--conf** or adjust the parameters in the **spark-defaults.conf** configuration file on the client.

.. table:: **Table 1** Parameter description

   +------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | Parameter                    | Scenario        | Description                                                                                                                                                                                   | Default Value   |
   +==============================+=================+===============================================================================================================================================================================================+=================+
   | spark.sql.tungsten.enabled   | /               | Type: Boolean                                                                                                                                                                                 | true            |
   |                              |                 |                                                                                                                                                                                               |                 |
   |                              |                 | -  If the value is **true**, tungsten is enabled. That is, the logic plan is equivalent to the codegeneration function, and the physical plan uses the corresponding tungsten execution plan. |                 |
   |                              |                 | -  If the value is **false**, tungsten is disabled.                                                                                                                                           |                 |
   +------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | spark.sql.codegen.wholeStage |                 | Type: Boolean                                                                                                                                                                                 | true            |
   |                              |                 |                                                                                                                                                                                               |                 |
   |                              |                 | -  If the value is **true**, codegeneration is enabled. That is, for some specified queries, the logic plan code will be generated dynamically when running.                                  |                 |
   |                              |                 | -  If the value is **false**, codegeneration is disabled and the existing static code is used.                                                                                                |                 |
   +------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+

.. note::

   #. To enable ExternalSort, you need to set **spark.sql.planner.externalSort** to **true** and **spark.sql.unsafe.enabled** to **false** or **spark.sql.codegen.wholeStage** to **false**.

   #. To enable TungstenAggregate, use either of the following methods:

      Set **spark.sql.codegen.wholeStage** and **spark.sql.unsafe.enabled** to **true** in the configuration file or CLI.

      If neither **spark.sql.codegen.wholeStage** nor **spark.sql.unsafe.enabled** is **true** or either of them is **true**, TungstenAggregate is enabled as long as **spark.sql.tungsten.enabled** is set to **true**.
