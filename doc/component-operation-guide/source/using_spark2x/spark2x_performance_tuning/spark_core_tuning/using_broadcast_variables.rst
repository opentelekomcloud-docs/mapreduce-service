:original_name: mrs_01_1979.html

.. _mrs_01_1979:

Using Broadcast Variables
=========================

Scenario
--------

Broadcast distributes data sets to each node. It allows data to be obtained locally when a data set is needed during a Spark task. If broadcast is not used, data serialization will be scheduled to tasks each time when a task requires data sets. It is time-consuming and makes the task get bigger.

#. If a data set will be used by each slice of a task, broadcast the data set to each node.
#. When small and big tables need to be joined, broadcast small tables to each node. This eliminates the shuffle operation, changing the join operation into a common operation.

Procedure
---------

Add the following code to broadcast the testArr data to each node:

.. code-block::

   def main(args: Array[String) {
     ...
     val testArr: Array[Long] = new Array[Long](200)
     val testBroadcast: Broadcast[Array[Long]] = sc.broadcast(testArr)
     val resultRdd: RDD[Long] = inpputRdd.map(input => handleData(testBroadcast, input))
     ...
   }

   def handleData(broadcast: Broadcast[Array[Long]], input: String) {
     val value = broadcast.value
     ...
   }
