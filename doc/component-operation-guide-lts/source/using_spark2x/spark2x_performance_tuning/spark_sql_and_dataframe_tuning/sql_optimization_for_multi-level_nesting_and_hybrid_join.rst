:original_name: mrs_01_2000.html

.. _mrs_01_2000:

SQL Optimization for Multi-level Nesting and Hybrid Join
========================================================

Scenario
--------

This section describes the optimization suggestions for SQL statements in multi-level nesting and hybrid join scenarios.

Prerequisites
-------------

The following provides an example of complex query statements:

.. code-block::

   elect
   s_name,
   count(1) as numwait
   from (
   select s_name from (
   select
   s_name,
   t2.l_orderkey,
   l_suppkey,
   count_suppkey,
   max_suppkey
   from
   test2 t2 right outer join (
   select
   s_name,
   l_orderkey,
   l_suppkey from (
   select
   s_name,
   t1.l_orderkey,
   l_suppkey,
   count_suppkey,
   max_suppkey
   from
   test1 t1 join (
   select
   s_name,
   l_orderkey,
   l_suppkey
   from
   orders o join (
   select
   s_name,
   l_orderkey,
   l_suppkey
   from
   nation n join supplier s
   on
   s.s_nationkey = n.n_nationkey
   and n.n_name = 'SAUDI ARABIA'
   join lineitem l
   on
   s.s_suppkey = l.l_suppkey
   where
   l.l_receiptdate > l.l_commitdate
   and l.l_orderkey is not null
   ) l1 on o.o_orderkey = l1.l_orderkey and o.o_orderstatus = 'F'
   ) l2 on l2.l_orderkey = t1.l_orderkey
   ) a
   where
   (count_suppkey > 1)
   or ((count_suppkey=1)
   and (l_suppkey <> max_suppkey))
   ) l3 on l3.l_orderkey = t2.l_orderkey
   ) b
   where
   (count_suppkey is null)
   or ((count_suppkey=1)
   and (l_suppkey = max_suppkey))
   ) c
   group by
   s_name
   order by
   numwait desc,
   s_name
   limit 100;

Procedure
---------

#. Analyze business.

   Analyze business to determine whether SQL statements can be simplified through measures, for example, by combining tables to reduce the number of nesting levels and join times.

#. If the SQL statements cannot be simplified, configure the driver memory.

   -  If SQL statements are executed through spark-submit or spark-sql, go to :ref:`3 <mrs_01_2000__en-us_topic_0000001173949962_l808aae986fc948d6903dc2cc981034dd>`.
   -  If SQL statements are executed through spark-beeline, go to :ref:`4 <mrs_01_2000__en-us_topic_0000001173949962_l156d16075fcf45fdb9aaea523ea81729>`.

#. .. _mrs_01_2000__en-us_topic_0000001173949962_l808aae986fc948d6903dc2cc981034dd:

   During execution of SQL statements, specify the **driver-memory** parameter. An example of SQL statements is as follows:

   **/spark-sql --master=local[4] --driver-memory=512M -f /tpch.sql**

#. .. _mrs_01_2000__en-us_topic_0000001173949962_l156d16075fcf45fdb9aaea523ea81729:

   Before running SQL statements, change the memory size as the system administrator.

   a. Log in to FusionInsight Manager and choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Configurations**.
   b. On the displayed page, click **All Configurations** and search for **SPARK_DRIVER_MEMORY**.
   c. Modify the **SPARK_DRIVER_MEMORY** parameter value to increase the memory size. The parameter value consists of two parts: memory size (an integer) and the unit (M or G), for example, **512M**.

Reference
---------

In the event of insufficient driver memory, the following error may be displayed during the query:

.. code-block::

   2018-02-11 09:13:14,683 | WARN  | Executor task launch worker for task 5 | Calling spill() on RowBasedKeyValueBatch. Will not spill but return 0. | org.apache.spark.sql.catalyst.expressions.RowBasedKeyValueBatch.spill(RowBasedKeyValueBatch.java:173)
   2018-02-11 09:13:14,682 | WARN  | Executor task launch worker for task 3 | Calling spill() on RowBasedKeyValueBatch. Will not spill but return 0. | org.apache.spark.sql.catalyst.expressions.RowBasedKeyValueBatch.spill(RowBasedKeyValueBatch.java:173)
   2018-02-11 09:13:14,704 | ERROR | Executor task launch worker for task 2 | Exception in task 2.0 in stage 1.0 (TID 2) | org.apache.spark.internal.Logging$class.logError(Logging.scala:91)
   java.lang.OutOfMemoryError: Unable to acquire 262144 bytes of memory, got 0
           at org.apache.spark.memory.MemoryConsumer.allocateArray(MemoryConsumer.java:100)
           at org.apache.spark.unsafe.map.BytesToBytesMap.allocate(BytesToBytesMap.java:791)
           at org.apache.spark.unsafe.map.BytesToBytesMap.<init>(BytesToBytesMap.java:208)
           at org.apache.spark.unsafe.map.BytesToBytesMap.<init>(BytesToBytesMap.java:223)
           at org.apache.spark.sql.execution.UnsafeFixedWidthAggregationMap.<init>(UnsafeFixedWidthAggregationMap.java:104)
           at org.apache.spark.sql.execution.aggregate.HashAggregateExec.createHashMap(HashAggregateExec.scala:307)
           at org.apache.spark.sql.catalyst.expressions.GeneratedClass$GeneratedIterator.agg_doAggregateWithKeys$(Unknown Source)
           at org.apache.spark.sql.catalyst.expressions.GeneratedClass$GeneratedIterator.processNext(Unknown Source)
           at org.apache.spark.sql.execution.BufferedRowIterator.hasNext(BufferedRowIterator.java:43)
           at org.apache.spark.sql.execution.WholeStageCodegenExec$$anonfun$8$$anon$1.hasNext(WholeStageCodegenExec.scala:381)
           at scala.collection.Iterator$$anon$11.hasNext(Iterator.scala:408)
           at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:126)
           at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:96)
           at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
           at org.apache.spark.scheduler.Task.run(Task.scala:99)
           at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:325)
           at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
           at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
           at java.lang.Thread.run(Thread.java:748)
