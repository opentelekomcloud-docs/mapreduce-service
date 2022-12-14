:original_name: mrs_01_24051.html

.. _mrs_01_24051:

Why Do Reduce Tasks Fail to Run in Some OSs After the Native Task Feature is Enabled?
=====================================================================================

Question
--------

After the Native Task feature is enabled, Reduce tasks fail to run in some OSs.

Answer
------

When **-Dmapreduce.job.map.output.collector.class=org.apache.hadoop.mapred.nativetask.NativeMapOutputCollectorDelegator** is executed to enable the Native Task feature during the running of MapReduce tasks that contain Reduce tasks, the tasks fail to run in some OSs, and the error message "version 'GLIBCXX_3.4.20' not found" is displayed in logs. The cause is that the GLIBCXX version of the OSs is too early. As a result, the libnativetask.so.1.0.0 library on which the feature depends cannot be loaded, leading to task failures.

Workaround:

Set **mapreduce.job.map.output.collector.class** to **org.apache.hadoop.mapred.MapTask$MapOutputBuffer**.
