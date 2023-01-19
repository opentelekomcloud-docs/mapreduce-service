:original_name: mrs_01_1791.html

.. _mrs_01_1791:

Why the Client Hangs During Job Running?
========================================

Question
--------

Why is the client unavailable when the MR ApplicationMaster or ResourceManager is moved to the D state during job running?

Answer
------

When a task is running, the MR ApplicationMaster or ResourceManager is moved to D state (uninterrupted sleep state) or T state (stopped state). The client waits to return the task running state, but the MR ApplicationMaster does not return. Therefore, the client remains in the waiting state.

To avoid the preceding scenario, use the **ipc.client.rpc.timeout** configuration item in the **core-site.xml** file to set the client timeout interval.

The value of this parameter is millisecond. The default value is **0**, indicating that no timeout occurs. The client timeout interval ranges from 0 ms to 2,147,483,647 ms.

.. note::

   -  If the Hadoop process is in the D state, restart the node where the process is located.
   -  The **core-site.xml** configuration file is stored in the **conf** directory of the client installation path, for example, **/opt/hadoopClient/Yarn/config**.
