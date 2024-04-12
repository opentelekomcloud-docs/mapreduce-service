:original_name: mrs_01_24224.html

.. _mrs_01_24224:

UDF Java and SQL Examples
=========================

UDF Java Example
----------------

.. code-block::

   package com.xxx.udf;
   import org.apache.flink.table.functions.ScalarFunction;
   public class UdfClass_UDF extends ScalarFunction {
       public int eval(String s) {
           return s.length();
       }
   }

UDF SQL Example
---------------

.. code-block::

   CREATE TEMPORARY FUNCTION udf as 'com.xxx..udf.UdfClass_UDF';
   CREATE TABLE udfSource (a VARCHAR) WITH ('connector' = 'datagen','rows-per-second'='1');
   CREATE TABLE udfSink (a VARCHAR,b int) WITH ('connector' = 'print');
   INSERT INTO
     udfSink
   SELECT
     a,
     udf(a)
   FROM
     udfSource;
