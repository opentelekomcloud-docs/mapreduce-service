:original_name: ALM-19006.html

.. _ALM-19006:

ALM-19006 HBase Replication Sync Failed
=======================================

Description
-----------

The alarm module checks the HBase DR data synchronization status every 30 seconds. When disaster recovery (DR) data fails to be synchronized to a standby cluster, the alarm is triggered.

When DR data synchronization succeeds, the alarm is cleared.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19006    Critical       Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

HBase data in a cluster fails to be synchronized to the standby cluster, causing data inconsistency between active and standby clusters.

Possible Causes
---------------

-  The HBase service on the standby cluster is abnormal.
-  A network exception occurs.

Procedure
---------

**Observe whether the system automatically clears the alarm.**

#. On the MRS Manager portal of the active cluster, click **O&M** > **Alarm** > **Alarms.**

#. In the alarm list, click the alarm to obtain alarm generation time from **Generated** of the alarm. Check whether the alarm has existed for five minutes.

   -  If yes, go to :ref:`4 <alm-19006__li2065263819413>`.
   -  If no, go to :ref:`3 <alm-19006__li5327925819413>`.

#. .. _alm-19006__li5327925819413:

   Wait five minutes and check whether the system automatically clears the alarm.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-19006__li2065263819413>`.

**Check the HBase service status of the standby cluster.**

4.  .. _alm-19006__li2065263819413:

    Log in to the MRS Manager portal of the active cluster, and click **O&M** > **Alarm** > **Alarms.**

5.  In the alarm list, click the alarm to obtain **HostName** from **Location**.

6.  Access the node where the HBase client of the active cluster resides as user **omm**.

    If the cluster uses a security mode, perform security authentication first and then access the **hbase shell** interface as user **hbase**.

    **cd /opt/client**

    **source ./bigdata_env**

    **kinit** *hbaseuser*

7.  Run the **status 'replication', 'source'** command to check the DR synchronization status of the faulty node.

    The DR synchronization status of a node is as follows.

    .. code-block::

       10-10-10-153:
       SOURCE: PeerID=abc, SizeOfLogQueue=0, ShippedBatches=2, ShippedOps=2, ShippedBytes=320, LogReadInBytes=1636, LogEditsRead=5, LogEditsFiltered=3, SizeOfLogToReplicate=0, TimeForLogToReplicate=0, ShippedHFiles=0, SizeOfHFileRefsQueue=0, AgeOfLastShippedOp=0, TimeStampsOfLastShippedOp=Mon Jul 18 09:53:28 CST 2016, Replication Lag=0, FailedReplicationAttempts=0
       SOURCE: PeerID=abc1, SizeOfLogQueue=0, ShippedBatches=1, ShippedOps=1, ShippedBytes=160, LogReadInBytes=1636, LogEditsRead=5, LogEditsFiltered=3, SizeOfLogToReplicate=0, TimeForLogToReplicate=0, ShippedHFiles=0, SizeOfHFileRefsQueue=0, AgeOfLastShippedOp=16788, TimeStampsOfLastShippedOp=Sat Jul 16 13:19:00 CST 2016, Replication Lag=16788, FailedReplicationAttempts=5

8.  Obtain **PeerID** corresponding to a record whose **FailedReplicationAttempts** value is greater than 0.

    In the preceding step, data on the faulty node 10-10-10-153 fails to be synchronized to a standby cluster whose **PeerID** is **abc1**.

9.  .. _alm-19006__li6555881219413:

    Run the **list_peers** command to find the cluster and the HBase instance corresponding to the **PeerID** value.

    .. code-block::

       PEER_ID CLUSTER_KEY STATE TABLE_CFS
       abc1 10.10.10.110,10.10.10.119,10.10.10.133:2181:/hbase2 ENABLED
       abc 10.10.10.110,10.10.10.119,10.10.10.133:2181:/hbase ENABLED

    In the preceding information, **/hbase2** indicates that data is synchronized to the HBase2 instance of the standby cluster.

10. In the service list of MRS Manager of the standby cluster, check whether the running status of the HBase instance obtained by using :ref:`9 <alm-19006__li6555881219413>` is **Normal**.

    -  If yes, go to :ref:`14 <alm-19006__li2284519319413>`.
    -  If no, go to :ref:`11 <alm-19006__li448244019413>`.

11. .. _alm-19006__li448244019413:

    In the alarm list, check whether the **ALM-19000 HBase Service Unavailable** alarm is generated.

    -  If yes, go to :ref:`12 <alm-19006__li2753337519413>`.
    -  If no, go to :ref:`14 <alm-19006__li2284519319413>`.

12. .. _alm-19006__li2753337519413:

    Follow troubleshooting procedures in **ALM-19000 HBase Service Unavailable** to rectify the fault.

13. Wait for a few minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-19006__li2284519319413>`.

**Check network connections between RegionServers on active and standby clusters.**

14. .. _alm-19006__li2284519319413:

    Log in to the MRS Manager portal of the active cluster, and click **O&M** > **Alarm** > **Alarms.**

15. .. _alm-19006__li3322104919413:

    In the alarm list, click the alarm to obtain **HostName** from **Location**.

16. Use the IP address obtained in :ref:`15 <alm-19006__li3322104919413>` to log in to a faulty RegionServer node as user **omm**.

17. Run the **ping** command to check whether network connections between the faulty RegionServer node and the host where RegionServer of the standby cluster resides are in the normal state.

    -  If yes, go to :ref:`20 <alm-19006__li342888619413>`.
    -  If no, go to :ref:`18 <alm-19006__li5820706019413>`.

18. .. _alm-19006__li5820706019413:

    Contact the network administrator to restore the network.

19. After the network is running properly, check whether the alarm is cleared in the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-19006__li342888619413>`.

**Collect fault information.**

20. .. _alm-19006__li342888619413:

    On the MRS Manager interface of active and standby clusters, choose **O&M** > **Log** > **Download**.

21. In the **Service** drop-down list box, select **HBase** in the required cluster.

22. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

23. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607922.png
