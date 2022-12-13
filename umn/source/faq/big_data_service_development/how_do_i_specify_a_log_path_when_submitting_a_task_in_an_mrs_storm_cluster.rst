:original_name: mrs_03_1127.html

.. _mrs_03_1127:

How Do I Specify a Log Path When Submitting a Task in an MRS Storm Cluster?
===========================================================================

You can modify the **/opt/Bigdata/MRS\_**\ *XXX* **/1\_**\ *XX* **\_Supervisor/etc/worker.xml** file on the streaming Core node of MRS, set the value of **filename** to the path, and restart the corresponding instance on Manager.

You are advised not to modify the default log configuration of MRS. Otherwise, the log system may become abnormal.
