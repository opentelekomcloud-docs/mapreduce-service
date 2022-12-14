:original_name: mrs_01_1964.html

.. _mrs_01_1964:

Configuring Vector-based ORC Data Reading
=========================================

Scenario
--------

ORC is a column-based storage format in the Hadoop ecosystem. It originates from Apache Hive and is used to reduce the Hadoop data storage space and accelerate the Hive query speed. Similar to Parquet, ORC is not a pure column-based storage format. In the ORC format, the entire table is split based on the row group, data in each row group is stored by column, and data is compressed as much as possible to reduce storage space consumption. Vector-based ORC data reading significantly improves the ORC data reading performance. In Spark2.3, SparkSQL supports vector-based ORC data reading (this function is supported in earlier Hive versions). Vector-based ORC data reading improves the data reading performance by multiple times.

This feature can be enabled by using the following parameter.

-  **spark.sql.orc.enableVectorizedReader**: specifies whether vector-based ORC data reading is supported. The default value is **true**.
-  **spark.sql.codegen.wholeStage**: specifies whether to compile all stages of multiple operations into a Java method. The default value is **true**.
-  **spark.sql.codegen.maxFields**: specifies the maximum number of fields (including nested fields) supported by all stages of codegen. The default value is **100**.
-  **spark.sql.orc.impl**: specifies whether Hive or Spark SQL native is used as the SQL execution engine to read ORC data. The default value is **hive**.

Parameters
----------

Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x**, click the **Configurations** tab and then **All Configurations**, and search for the following parameters.

+--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+---------------+----------------+
| Parameter                            | Description                                                                                                                        | Default Value | Value Range    |
+======================================+====================================================================================================================================+===============+================+
| spark.sql.orc.enableVectorizedReader | Specifies whether vector-based ORC data reading is supported. The default value is **true**.                                       | true          | [true,false]   |
+--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+---------------+----------------+
| spark.sql.codegen.wholeStage         | Specifies whether to compile all stages of multiple operations into a Java method. The default value is **true**.                  | true          | [true,false]   |
+--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+---------------+----------------+
| spark.sql.codegen.maxFields          | Specifies the maximum number of fields (including nested fields) supported by all stages of codegen. The default value is **100**. | 100           | Greater than 0 |
+--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+---------------+----------------+
| spark.sql.orc.impl                   | Specifies whether Hive or Spark SQL native is used as the SQL execution engine to read ORC data. The default value is **hive**.    | hive          | [hive,native]  |
+--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+---------------+----------------+

.. note::

   #. To use vector-based ORC data reading of SparkSQL, the following conditions must be met:

      -  **spark.sql.orc.enableVectorizedReader** must be set to **true** (default value). Generally, the value is not changed.
      -  **spark.sql.codegen.wholeStage** must be set to **true** (default value). Generally, the value is not changed.
      -  The value of **spark.sql.codegen.maxFields** must be greater than or equal to the number of columns in scheme.
      -  All data is of the AtomicType. Specifically, data is not null or of the UDT, array, or map type. If there is data of the preceding types, expected performance cannot be obtained.
      -  **spark.sql.orc.impl** must be set to **native**. The default value is **hive**.

   #. If a task is submitted using the client, modification of the following parameters takes effect only after you download the client again: **spark.sql.orc.enableVectorizedReader**, **spark.sql.codegen.wholeStage**, **spark.sql.codegen.maxFields**, and **spark.sql.orc.impl**.
