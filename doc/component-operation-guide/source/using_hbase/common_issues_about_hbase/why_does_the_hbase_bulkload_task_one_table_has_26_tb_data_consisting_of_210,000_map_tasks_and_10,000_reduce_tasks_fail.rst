:original_name: mrs_01_1643.html

.. _mrs_01_1643:

Why Does the HBase BulkLoad Task (One Table Has 26 TB Data) Consisting of 210,000 Map Tasks and 10,000 Reduce Tasks Fail?
=========================================================================================================================

Question
--------

The HBase bulkLoad task (a single table contains 26 TB data) has 210,000 maps and 10,000 reduce tasks (in MRS 3.x or later), and the task fails.

Answer
------

**ZooKeeper I/O bottleneck observation methods:**

#. On the monitoring page of Manager, check whether the number of ZooKeeper requests on a single node exceeds the upper limit.
#. View ZooKeeper and HBase logs to check whether a large number of I/O Exception Timeout or SocketTimeout Exception exceptions occur.

**Optimization suggestions:**

#. Change the number of ZooKeeper instances to 5 or more. You are advised to set **peerType** to **observer** to increase the number of observers.
#. Control the number of concurrent maps of a single task or reduce the memory for running tasks on each node to lighten the node load.
#. Upgrade ZooKeeper data disks, such as SSDs.
