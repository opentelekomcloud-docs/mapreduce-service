:original_name: mrs_08_00163.html

.. _mrs_08_00163:

Flume Enhanced Open Source Features
===================================


Flume Enhanced Open Source Features
-----------------------------------

-  Improving transmission speed: Multiple lines instead of only one line of data can be specified as an event. This improves the efficiency of code execution and reduces the times of disk writes.
-  Transferring ultra-large binary files: According to the current memory usage, Flume automatically adjusts the memory used for transferring ultra-large binary files to prevent out-of-memory.
-  Supporting the customization of preparations before and after transmission: Flume supports customized scripts to be run before or after transmission for making preparations.
-  Managing client alarms: Flume receives Flume client alarms through MonitorServer and reports the alarms to the alarm management center on MRS Manager.
