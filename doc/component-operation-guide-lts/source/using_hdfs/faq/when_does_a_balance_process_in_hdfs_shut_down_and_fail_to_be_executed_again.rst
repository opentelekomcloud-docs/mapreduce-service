:original_name: mrs_01_1707.html

.. _mrs_01_1707:

When Does a Balance Process in HDFS, Shut Down and Fail to be Executed Again?
=============================================================================

Question
--------

After I start a Balance process in HDFS, the process is shut down abnormally. If I attempt to execute the Balance process again, it fails again.

Answer
------

After a Balance process is executed in HDFS, another Balance process can be executed only after the **/system/balancer.id** file is automatically released.

However, if a Balance process is shut down abnormally, the **/system/balancer.id** has not been released when the Balance is executed again, which triggers the **append /system/balancer.id** operation.

-  If the time spent on releasing the **/system/balancer.id** file exceeds the soft-limit lease period 60 seconds, executing the Balance process again triggers the append operation, which preempts the lease. The last block is in construction or under recovery status, which triggers the block recovery operation. The **/system/balancer.id** file cannot be closed until the block recovery completes. Therefore, the append operation fails.

   After the **append /system/balancer.id** operation fails, the exception message **RecoveryInProgressException** is displayed.

   .. code-block::

      org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.protocol.RecoveryInProgressException): Failed to APPEND_FILE /system/balancer.id for DFSClient because lease recovery is in progress. Try again later.

-  If the time spent on releasing the **/system/balancer.id** file is within 60 seconds, the original client continues to own the lease and the exception AlreadyBeingCreatedException occurs and null is returned to the client. The following exception message is displayed on the client:

   .. code-block::

      java.io.IOException: Cannot create any NameNode Connectors.. Exiting...

Either of the following methods can be used to solve the problem:

-  Execute the Balance process again after the hard-limit lease period expires for 1 hour, when the original client has released the lease.
-  Delete the **/system/balancer.id** file before executing the Balance process again.
