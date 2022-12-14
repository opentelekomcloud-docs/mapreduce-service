:original_name: mrs_01_1419.html

.. _mrs_01_1419:

Suggestions for Creating CarbonData Tables
==========================================

Scenario
--------

This section provides suggestions based on more than 50 test cases to help you create CarbonData tables with higher query performance.

.. table:: **Table 1** Columns in the CarbonData table

   =========== ============= =========== ===========
   Column name Data type     Cardinality Attribution
   =========== ============= =========== ===========
   msisdn      String        30 million  dimension
   BEGIN_TIME  bigint        10,000      dimension
   host        String        1 million   dimension
   dime_1      String        1,000       dimension
   dime_2      String        500         dimension
   dime_3      String        800         dimension
   counter_1   numeric(20,0) NA          measure
   ...         ...           NA          measure
   counter_100 numeric(20,0) NA          measure
   =========== ============= =========== ===========

Procedure
---------

-  If the to-be-created table contains a column that is frequently used for filtering, for example, this column is used in more than 80% of filtering scenarios,

   implement optimization as follows:

   Place this column in the first column of **sort_columns**.

   For example, if **msisdn** is the most frequently used filter criterion in a query, it is placed in the first column. Run the following command to create a table. The query performance is good if **msisdn** is used as the filter condition.

   .. code-block::

      create table carbondata_table(
          msisdn String,
          ...
          )STORED AS carbondata TBLPROPERTIES ('SORT_COLUMS'='msisdn');

-  If the to-be-created table has multiple columns which are frequently used to filter the results,

   implement optimization as follows:

   Create an index for the columns.

   For example, if **msisdn**, **host**, and **dime_1** are frequently used columns, the **sort_columns** column sequence is "dime_1-> host-> msisdn..." based on cardinality. Run the following command to create a table. The following command can improve the filtering performance of **dime_1**, **host**, and **msisdn**.

   .. code-block::

      create table carbondata_table(
          dime_1 String,
          host String,
          msisdn String,
          dime_2 String,
          dime_3 String,
          ...
          )STORED AS carbondata
      TBLPROPERTIES ('SORT_COLUMS'='dime_1,host,msisdn');

-  If the frequency of each column used for filtering is similar,

   implement optimization as follows:

   **sort_columns** is sorted in ascending order of cardinality.

   Run the following command to create a table:

   .. code-block::

      create table carbondata_table(
          Dime_1 String,
          BEGIN_TIME bigint,
          HOST String,
          MSISDN String,
          ...
          )STORED AS carbondata
      TBLPROPERTIES ('SORT_COLUMS'='dime_2,dime_3,dime_1, BEGIN_TIME,host,msisdn');

-  Create tables in ascending order of cardinalities. Then create secondary indexes for columns with more cardinalities. The statement for creating an index is as follows:

   .. code-block::

      create index carbondata_table_index_msidn on tablecarbondata_table (
      MSISDN String) as 'carbondata' PROPERTIES ('table_blocksize'='128');
      create index carbondata_table_index_host on tablecarbondata_table (
      host String) as 'carbondata' PROPERTIES ('table_blocksize'='128');

-  For columns of measure type, not requiring high accuracy, the numeric (20,0) data type is not required. You are advised to use the double data type to replace the numeric (20,0) data type to enhance query performance.

   The result of performance analysis of test-case shows reduction in query execution time from 15 to 3 seconds, thereby improving performance by nearly 5 times. The command for creating a table is as follows:

   .. code-block::

      create table carbondata_table(
          Dime_1 String,
          BEGIN_TIME bigint,
          HOST String,
          MSISDN String,
          counter_1 double,
          counter_2 double,
          ...
          counter_100 double,
          )STORED AS carbondata
      ;

-  If values (**start_time** for example) of a column are incremental:

   For example, if data is loaded to CarbonData every day, **start_time** is incremental for each load. In this case, it is recommended that the **start_time** column be put at the end of **sort_columns**, because incremental values are efficient in using min/max index. The command for creating a table is as follows:

   .. code-block::

      create table carbondata_table(
          Dime_1 String,
          HOST String,
          MSISDN String,
          counter_1 double,
          counter_2 double,
          BEGIN_TIME bigint,
          ...
          counter_100 double,
          )STORED AS carbondata
          TBLPROPERTIES ( 'SORT_COLUMS'='dime_2,dime_3,dime_1..BEGIN_TIME');
