:original_name: mrs_01_24121.html

.. _mrs_01_24121:

Hive Supporting ZSTD Compression Formats
========================================

Zstandard (ZSTD) is an open-source lossless data compression algorithm. Its compression performance and compression ratio are better than those of other compression algorithms supported by Hadoop. Hive with this feature supports tables in ZSTD compression formats. The ZSTD compression formats supported by Hive include ORC, RCFile, TextFile, JsonFile, Parquet, Squence, and CSV.

You can create a table in ZSTD compression format as follows:

-  To create a table in ORC format, specify **TBLPROPERTIES("orc.compress"="zstd")**.

   **create table tab_1(...) stored as orc TBLPROPERTIES("orc.compress"="zstd");**

-  To create a table in Parquet format, specify **TBLPROPERTIES("parquet.compression"="zstd")**.

   **create table tab_2(...) stored as parquet TBLPROPERTIES("parquet.compression"="zstd");**

-  To create a table in other formats or common formats, run the following commands to set the **mapreduce.map.output.compress.codec** and **mapreduce.output.fileoutputformat.compress.codec** parameters to **org.apache.hadoop.io.compress.ZStandardCode**.

   **set hive.exec.compress.output=true;**

   **set mapreduce.map.output.compress=true;**

   **set mapreduce.map.output.compress.codec=org.apache.hadoop.io.compress.ZStandardCodec;**

   **set mapreduce.output.fileoutputformat.compress=true;**

   **set mapreduce.output.fileoutputformat.compress.codec=org.apache.hadoop.io.compress.ZStandardCodec;**

   **set hive.exec.compress.intermediate=true;**

   **create table tab_3(...) stored as textfile;**

.. note::

   The SQL operations on a table compressed using ZSTD are the same as those on a common compressed table. A table compressed using ZSTD supports addition, deletion, query, and aggregation SQL operations.
