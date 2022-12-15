:original_name: mrs_01_2053.html

.. _mrs_01_2053:

Why does Spark Streaming Application Fail to Restart from Checkpoint When It Creates an Input Stream Without Output Logic?
==========================================================================================================================

Question
--------

Spark Streaming application creates one input stream without output logic. The application fails to restart from checkpoint and an error will be shown like below:

.. code-block::

   17/04/24 10:13:57 ERROR Utils: Exception encountered
   java.lang.NullPointerException
   at org.apache.spark.streaming.dstream.DStreamCheckpointData$$anonfun$writeObject$1.apply$mcV$sp(DStreamCheckpointData.scala:125)
   at org.apache.spark.streaming.dstream.DStreamCheckpointData$$anonfun$writeObject$1.apply(DStreamCheckpointData.scala:123)
   at org.apache.spark.streaming.dstream.DStreamCheckpointData$$anonfun$writeObject$1.apply(DStreamCheckpointData.scala:123)
   at org.apache.spark.util.Utils$.tryOrIOException(Utils.scala:1195)
   at org.apache.spark.streaming.dstream.DStreamCheckpointData.writeObject(DStreamCheckpointData.scala:123)
   at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
   at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
   at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
   at java.lang.reflect.Method.invoke(Method.java:498)
   at java.io.ObjectStreamClass.invokeWriteObject(ObjectStreamClass.java:1028)
   at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1496)
   at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1432
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1178)
   at java.io.ObjectOutputStream.defaultWriteFields(ObjectOutputStream.java:1548)
   at java.io.ObjectOutputStream.defaultWriteObject(ObjectOutputStream.java:441)
   at org.apache.spark.streaming.dstream.DStream$$anonfun$writeObject$1.apply$mcV$sp(DStream.scala:515)
   at org.apache.spark.streaming.dstream.DStream$$anonfun$writeObject$1.apply(DStream.scala:510)
   at org.apache.spark.streaming.dstream.DStream$$anonfun$writeObject$1.apply(DStream.scala:510)
   at org.apache.spark.util.Utils$.tryOrIOException(Utils.scala:1195)
   at org.apache.spark.streaming.dstream.DStream.writeObject(DStream.scala:510)
   at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
   at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
   at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
   at java.lang.reflect.Method.invoke(Method.java:498)
   at java.io.ObjectStreamClass.invokeWriteObject(ObjectStreamClass.java:1028)
   at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1496)
   at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1432
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1178)
   at java.io.ObjectOutputStream.writeArray(ObjectOutputStream.java:1378)
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1174)
   at java.io.ObjectOutputStream.defaultWriteFields(ObjectOutputStream.java:1548)
   at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1509)
   at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1432
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1178)
   at java.io.ObjectOutputStream.defaultWriteFields(ObjectOutputStream.java:1548)
   at java.io.ObjectOutputStream.defaultWriteObject(ObjectOutputStream.java:441)
   at org.apache.spark.streaming.DStreamGraph$$anonfun$writeObject$1.apply$mcV$sp(DStreamGraph.scala:191)
   at org.apache.spark.streaming.DStreamGraph$$anonfun$writeObject$1.apply(DStreamGraph.scala:186)
   at org.apache.spark.streaming.DStreamGraph$$anonfun$writeObject$1.apply(DStreamGraph.scala:186)
   at org.apache.spark.util.Utils$.tryOrIOException(Utils.scala:1195)
   at org.apache.spark.streaming.DStreamGraph.writeObject(DStreamGraph.scala:186
   at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
   at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
   at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
   at java.lang.reflect.Method.invoke(Method.java:498)
   at java.io.ObjectStreamClass.invokeWriteObject(ObjectStreamClass.java:1028)
   at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1496)
   at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1432
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1178)
   at java.io.ObjectOutputStream.defaultWriteFields(ObjectOutputStream.java:1548)
   at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1509)
   at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1432
   at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1178)
   at java.io.ObjectOutputStream.writeObject(ObjectOutputStream.java:348)
   at org.apache.spark.streaming.Checkpoint$$anonfun$serialize$1.apply$mcV$sp(Checkpoint.scala:142)
   at org.apache.spark.streaming.Checkpoint$$anonfun$serialize$1.apply(Checkpoint.scala:142)
   at org.apache.spark.streaming.Checkpoint$$anonfun$serialize$1.apply(Checkpoint.scala:142)
   at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1230)
   at org.apache.spark.streaming.Checkpoint$.serialize(Checkpoint.scala:143)
   at org.apache.spark.streaming.StreamingContext.validate(StreamingContext.scala:566)
   at org.apache.spark.streaming.StreamingContext.liftedTree1$1(StreamingContext.scala:612)
   at org.apache.spark.streaming.StreamingContext.start(StreamingContext.scala:611)
   at com.spark.test.kafka08LifoTwoInkfk$.main(kafka08LifoTwoInkfk.scala:21)
   at com.spark.test.kafka08LifoTwoInkfk.main(kafka08LifoTwoInkfk.scala)
   at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
   at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
   at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
   at java.lang.reflect.Method.invoke(Method.java:498)
   at org.apache.spark.deploy.SparkSubmit$.org$apache$spark$deploy$SparkSubmit$$runMain(SparkSubmit.scala:772)
   at org.apache.spark.deploy.SparkSubmit$.doRunMain$1(SparkSubmit.scala:183)
   at org.apache.spark.deploy.SparkSubmit$.submit(SparkSubmit.scala:208)
   at org.apache.spark.deploy.SparkSubmit$.main(SparkSubmit.scala:123)
   at org.apache.spark.deploy.SparkSubmit.main(SparkSubmit.scala)

Answer
------

When Streaming Context starts, DStream checkpoint object of application should be serialized with application set to checkpoint and Dstream context will be used during this serialization.

Dstream.context is the Dstream which Streaming Context relies on to check reversely from output Stream, set the context one by one. If Spark Streaming application creates one input stream which does not have output logic, there will be no context set for the input stream. 'NullPointerException' will be reported during serialization.

Solution: If there is no input logic for the output stream in the application, delete the input stream in the code or add the relevant output logic for that input stream.
