:original_name: mrs_01_1644.html

.. _mrs_01_1644:

How Do I Restore a Region in the RIT State for a Long Time?
===========================================================

Question
--------

How do I restore a region in the RIT state for a long time?

Answer
------

Log in to the HMaster Web UI, choose **Procedure & Locks** in the navigation tree, and check whether any process ID is in the **Waiting** state. If yes, run the following command to release the procedure lock:

**hbase hbck -j** *Client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar bypass -o** *pid*

Check whether the state is in the **Bypass** state. If the procedure on the UI is always in **RUNNABLE(Bypass)** state, perform an active/standby switchover. Run the **assigns** command to bring the region online again.

**hbase hbck -j** *Client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar assigns -o** *regionName*
