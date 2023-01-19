:original_name: mrs_01_1953.html

.. _mrs_01_1953:

Configuring the Compression Format of a Parquet Table
=====================================================

Scenarios
---------

The compression format of a Parquet table can be configured as follows:

#. If the Parquet table is a partitioned one, set the **parquet.compression** parameter of the Parquet table to specify the compression format. For example, set **tblproperties** in the table creation statement: **"parquet.compression"="snappy"**.
#. If the Parquet table is a non-partitioned one, set the **spark.sql.parquet.compression.codec** parameter to specify the compression format. The configuration of the **parquet.compression** parameter is invalid, because the value of the **spark.sql.parquet.compression.codec** parameter is read by the **parquet.compression** parameter. If the **spark.sql.parquet.compression.codec** parameter is not configured, the default value is **snappy** and will be read by the **parquet.compression** parameter.

Therefore, the **spark.sql.parquet.compression.codec** parameter can only be used to set the compression format of a non-partitioned Parquet table.

Configuration parameters
------------------------

**Navigation path for setting parameters:**

On Manager, choose **Cluster > *Name of the desired cluster* > Service** > **Spark2x** > **Configuration**. Click **All Configurations** and enter a parameter name in the search box.

.. table:: **Table 1** Parameter description

   +-------------------------------------+------------------------------------------------------------------------+---------------+
   | Parameter                           | Description                                                            | Default Value |
   +=====================================+========================================================================+===============+
   | spark.sql.parquet.compression.codec | Used to set the compression format of a non-partitioned Parquet table. | snappy        |
   +-------------------------------------+------------------------------------------------------------------------+---------------+
