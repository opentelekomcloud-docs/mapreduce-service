:original_name: mrs_01_24227.html

.. _mrs_01_24227:

UDTF Java and SQL Examples
==========================

UDTF Java Example
-----------------

.. code-block::

   package com.xxx.udf;
   import org.apache.flink.api.java.tuple.Tuple2;
   import org.apache.flink.table.functions.TableFunction;
   public class UdfClass_UDTF extends TableFunction<Tuple2<String, Integer>> {
       public void eval(String str) {
           Tuple2<String, Integer> tuple2 = Tuple2.of(str, str.length());
           collect(tuple2);
       }
   }

UDTF SQL Example
----------------

.. code-block::

   CREATE TEMPORARY FUNCTION udtf as 'com.xxx.udf.UdfClass_UDTF';
   CREATE TABLE udfSource (a VARCHAR) WITH ('connector' = 'datagen','rows-per-second'='1');
   CREATE TABLE udfSink (b VARCHAR,c int) WITH ('connector' = 'print');
   INSERT INTO
     udfSink
   SELECT
     str,
     strLength
   FROM
     udfSource,lateral table(udtf(udfSource.a)) as T(str,strLength);
