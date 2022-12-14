:original_name: mrs_01_24117.html

.. _mrs_01_24117:

Hive Configuration Problems
===========================

-  The error message "java.lang.OutOfMemoryError: Java heap space." is displayed during Hive SQL execution.

   Solution:

   -  For MapReduce tasks, increase the values of the following parameters:

      **set mapreduce.map.memory.mb=8192;**

      **set mapreduce.map.java.opts=-Xmx6554M;**

      **set mapreduce.reduce.memory.mb=8192;**

      **set mapreduce.reduce.java.opts=-Xmx6554M;**

   -  For Tez tasks, increase the value of the following parameter:

      **set hive.tez.container.size=8192;**

-  After a column name is changed to a new one using the Hive SQL **as** statement, the error message "Invalid table alias or column reference 'xxx'." is displayed when the original column name is used for compilation.

   Solution: Run the **set hive.cbo.enable=true;** statement.

-  The error message "Unsupported SubQuery Expression 'xxx': Only SubQuery expressions that are top level conjuncts are allowed." is displayed during Hive SQL subquery compilation.

   Solution: Run the **set hive.cbo.enable=true;** statement.

-  The error message "CalciteSubquerySemanticException [Error 10249]: Unsupported SubQuery Expression Currently SubQuery expressions are only allowed as Where and Having Clause predicates." is displayed during Hive SQL subquery compilation.

   Solution: Run the **set hive.cbo.enable=true;** statement.

-  The error message "Error running query: java.lang.AssertionError: Cannot add expression of different type to set." is displayed during Hive SQL compilation.

   Solution: Run the **set hive.cbo.enable=false;** statement.

-  The error message "java.lang.NullPointerException at org.apache.hadoop.hive.ql.udf.generic.GenericUDAFComputeStats$GenericUDAFNumericStatsEvaluator.init." is displayed during Hive SQL execution.

   Solution: Run the **set hive.map.aggr=false;** statement.

-  When **hive.auto.convert.join** is set to **true** (enabled by default) and **hive.optimize.skewjoin** is set to **true**, the error message "ClassCastException org.apache.hadoop.hive.ql.plan.ConditionalWork cannot be cast to org.apache.hadoop.hive.ql.plan.MapredWork" is displayed.

   Solution: Run the **set hive.optimize.skewjoin=false;** statement.

-  When **hive.auto.convert.join** is set to **true** (enabled by default), **hive.optimize.skewjoin** is set to **true**, and **hive.exec.parallel** is set to **true**, the error message "java.io.FileNotFoundException: File does not exist:xxx/reduce.xml" is displayed.

   Solution:

   -  Method 1: Switch the execution engine to Tez. For details, see :ref:`Switching the Hive Execution Engine to Tez <mrs_01_1750>`.
   -  Method 2: Run the **set hive.exec.parallel=false;** statement.
   -  Method 3: Run the **set hive.auto.convert.join=false;** statement.

-  Eerror message "NullPointerException at org.apache.hadoop.hive.ql.exec.CommonMergeJoinOperator.mergeJoinComputeKeys" is displayed when Hive on Tez executes bucket map join.

   Solution: Run the **set tez.am.container.reuse.enabled=false;** statement.
