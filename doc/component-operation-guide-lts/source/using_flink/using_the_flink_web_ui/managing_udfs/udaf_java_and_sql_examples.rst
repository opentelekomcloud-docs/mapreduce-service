:original_name: mrs_01_24225.html

.. _mrs_01_24225:

UDAF Java and SQL Examples
==========================

UDAF Java Example
-----------------

.. code-block::

   package com.xxx.udf;
   import org.apache.flink.table.functions.AggregateFunction;
   public class UdfClass_UDAF {
       public static class AverageAccumulator  {
           public int sum;
       }
       public static class Average extends AggregateFunction<Integer, AverageAccumulator> {
           public void accumulate(AverageAccumulator acc, Integer value) {
               acc.sum += value;
           }
           @Override
           public Integer getValue(AverageAccumulator acc) {
               return acc.sum;
           }
           @Override
           public AverageAccumulator createAccumulator() {
               return new AverageAccumulator();
           }
       }
   }

UDAF SQL Example
----------------

.. code-block::

   CREATE TEMPORARY FUNCTION udaf as 'com.xxx.udf.UdfClass_UDAF$Average';
   CREATE TABLE udfSource (a int) WITH ('connector' = 'datagen','rows-per-second'='1','fields.a.min'='1','fields.a.max'='3');
   CREATE TABLE udfSink (b int,c int) WITH ('connector' = 'print');
   INSERT INTO
     udfSink
   SELECT
     a,
     udaf(a)
   FROM
     udfSource group by a;
