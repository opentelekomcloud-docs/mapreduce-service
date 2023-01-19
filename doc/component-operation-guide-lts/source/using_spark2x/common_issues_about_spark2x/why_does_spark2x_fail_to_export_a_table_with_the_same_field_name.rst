:original_name: mrs_01_2059.html

.. _mrs_01_2059:

Why Does Spark2x Fail to Export a Table with the Same Field Name?
=================================================================

Question
--------

The following code fails to be executed on spark-shell of Spark2x:

.. code-block::

   val acctId = List(("49562", "Amal", "Derry"), ("00000", "Fred", "Xanadu"))
   val rddLeft = sc.makeRDD(acctId)
   val dfLeft = rddLeft.toDF("Id", "Name", "City")
   //dfLeft.show
   val acctCustId = List(("Amal", "49562", "CO"), ("Dave", "99999", "ZZ"))
   val rddRight = sc.makeRDD(acctCustId)
   val dfRight = rddRight.toDF("Name", "CustId", "State")
   //dfRight.show
   val dfJoin = dfLeft.join(dfRight, dfLeft("Id") === dfRight("CustId"), "outer")
   dfJoin.show
   dfJoin.repartition(1).write.format("com.databricks.spark.csv").option("delimiter", "\t").option("header", "true").option("treatEmptyValuesAsNulls", "true").option("nullValue", "").save("/tmp/outputDir")

Answer
------

In Spark2x, the duplicate field name of the **join** statement is checked. You need to modify the code to ensure that no duplicate field exists in the saved data.
