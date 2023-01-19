:original_name: mrs_01_1467.html

.. _mrs_01_1467:

Why Do I Fail to Create a Hive Table?
=====================================

Question
--------

Why do I fail to create a hive table?

Answer
------

Creating a Hive table fails, when source table or sub query has more number of partitions. The implementation of the query requires a lot of tasks, then the number of files will be output a lot, resulting OOM in Driver.

It can be solved by using **distribute by** on suitable cardinality(distinct values) column in the statement of Hive table creation.

**distribute by** clause limits number of hive table partitions. It considers cardinality of given column or **spark.sql.shuffle.partitions** which ever is minimal. For example, if **spark.sql.shuffle.partitions** is 200, but cardinality of column is 100, out files is 200, but the other 100 files are empty. So using very low cardinality column like 1 will cause data skew and will effect later query distribution.

So we suggest using the column with cardinality greater than **spark.sql.shuffle.partitions**. It can be greater than 2 to 3 times.

Example:

**create table hivetable1 as select \* from sourcetable1 distribute by col_age;**
