:original_name: mrs_01_0954.html

.. _mrs_01_0954:

Using the Hive Column Encryption Function
=========================================

Scenario
--------

Hive supports encryption of one or more columns in a table. When creating a Hive table, you can specify the columns to be encrypted and encryption algorithm. When data is inserted into the table using the insert statement, the related columns are encrypted. Column encryption can be performed in HDFS tables of only the TextFile and SequenceFile file formats. Hive column encryption does not support the view and Hive over HBase scenarios.

Hive supports two column encryption algorithms, which can be specified during table creation:

-  AES (the encryption class is org.apache.hadoop.hive.serde2.AESRewriter)
-  SMS4 (the encryption class is org.apache.hadoop.hive.serde2.SMS4Rewriter)

.. note::

   *When you import data from a common Hive table into a Hive column encryption table, you are advised to delete the original data from the common Hive table as long as doing this does not affect other services. The reason is that retaining an unencrypted table is a security risk.*

Operation Procedure
-------------------

#. Specify the column to be encrypted and encryption algorithm when creating a table.

   **create table\ <[db_name.]table_name> (<col_name1> <data_type> ,<col_name2> <data_type>,<col_name3> <data_type>,<col_name4> <data_type>) ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe' WITH SERDEPROPERTIES ('column.encode.columns'='<col_name2>,<col_name3>', 'column.encode.classname'='org.apache.hadoop.hive.serde2.AESRewriter')STORED AS TEXTFILE;**

   Alternatively, use the following statement:

   **create table <[db_name.]table_name> (<col_name1> <data_type> ,<col_name2> <data_type>,<col_name3> <data_type>,<col_name4> <data_type>) ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe' WITH SERDEPROPERTIES ('column.encode.indices'='1,2', 'column.encode.classname'='org.apache.hadoop.hive.serde2.SMS4Rewriter') STORED AS TEXTFILE;**

   .. note::

      -  The numbers used to specify encryption columns start from 0. 0 indicates column 1, 1 indicates column 2, and so on.
      -  When creating a table with encrypted columns, ensure that the directory where the table resides is empty.

#. Insert data into the table using the insert statement.

   Assume that the test table exists and contains data.

   **insert into table <table_name> select <col_list> from test;**
