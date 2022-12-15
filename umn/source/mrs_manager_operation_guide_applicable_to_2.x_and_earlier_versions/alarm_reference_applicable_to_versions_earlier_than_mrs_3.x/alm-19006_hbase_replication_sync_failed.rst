:original_name: alm_19006.html

.. _alm_19006:

ALM-19006 HBase Replication Sync Failed
=======================================

Description
-----------

This alarm is generated when disaster recovery (DR) data fails to be synchronized to a standby cluster.

This alarm is cleared when DR data synchronization succeeds.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19006    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

HBase data in a cluster fails to be synchronized to the standby cluster, causing data inconsistency between active and standby clusters.

Possible Causes
---------------

-  The HBase service on the standby cluster is abnormal.
-  The network is abnormal.

Procedure
---------

#. Observe whether the system automatically clears the alarm.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, click the alarm to obtain alarm generation time from **Generated Time** in **Alarm Details**. Check whether the alarm has existed for over 5 minutes.

      -  If yes, go to :ref:`2.a <alm_19006__en-us_topic_0191813928_li1255962015108>`.
      -  If no, go to :ref:`1.c <alm_19006__en-us_topic_0191813928_step3>`.

   c. .. _alm_19006__en-us_topic_0191813928_step3:

      Wait 5 minutes and check whether the alarm is automatically cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_19006__en-us_topic_0191813928_li1255962015108>`.

#. Check the HBase service status of the standby cluster.

   a. .. _alm_19006__en-us_topic_0191813928_li1255962015108:

      Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, click the alarm and obtain **HostName** from **Location** in **Alarm Details**.

   c. Log in to the node where the HBase client of the active cluster is located. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   d. Run the **status 'replication', 'source'** command to check the synchronization status of the faulty node.

      The synchronization status of a node is as follows.

      .. code-block::

         10-10-10-153:
          SOURCE: PeerID=abc, SizeOfLogQueue=0, ShippedBatches=2, ShippedOps=2, ShippedBytes=320, LogReadInBytes=1636, LogEditsRead=5, LogEditsFiltered=3, SizeOfLogToReplicate=0, TimeForLogToReplicate=0, ShippedHFiles=0, SizeOfHFileRefsQueue=0, AgeOfLastShippedOp=0, TimeStampsOfLastShippedOp=Mon Jul 18 09:53:28 CST 2016, Replication Lag=0, FailedReplicationAttempts=0
          SOURCE: PeerID=abc1, SizeOfLogQueue=0, ShippedBatches=1, ShippedOps=1, ShippedBytes=160, LogReadInBytes=1636, LogEditsRead=5, LogEditsFiltered=3, SizeOfLogToReplicate=0, TimeForLogToReplicate=0, ShippedHFiles=0, SizeOfHFileRefsQueue=0, AgeOfLastShippedOp=16788, TimeStampsOfLastShippedOp=Sat Jul 16 13:19:00 CST 2016, Replication Lag=16788, FailedReplicationAttempts=5

   e. Obtain **PeerID** corresponding to a record whose **FailedReplicationAttempts** value is greater than 0.

      In the preceding step, data on the faulty node **10-10-10-153** fails to be synchronized to a standby cluster whose **PeerID** is **abc1**.

   f. .. _alm_19006__en-us_topic_0191813928_peerid:

      Run the **list_peers** command to find the cluster and the HBase instance corresponding to **PeerID**.

      .. code-block::

         PEER_ID CLUSTER_KEY STATE TABLE_CFS
          abc1 10.10.10.110,10.10.10.119,10.10.10.133:24002:/hbase2 ENABLED
          abc 10.10.10.110,10.10.10.119,10.10.10.133:24002:/hbase ENABLED

      In the preceding information, **/hbase2** indicates that data is synchronized to the HBase2 instance of the standby cluster.

   g. In the service list of the standby cluster, check whether the health status of the HBase instance obtained in :ref:`2.f <alm_19006__en-us_topic_0191813928_peerid>` is **Good**.

      -  If yes, go to :ref:`3.a <alm_19006__en-us_topic_0191813928_li594194191119>`.
      -  If no, go to :ref:`2.h <alm_19006__en-us_topic_0191813928_alm-19000>`.

   h. .. _alm_19006__en-us_topic_0191813928_alm-19000:

      In the alarm list, check whether the alarm ALM-19000 HBase Service Unavailable exists.

      -  If yes, go to :ref:`2.i <alm_19006__en-us_topic_0191813928_aalm-19006_mmccppss_process>`.
      -  If no, go to :ref:`3.a <alm_19006__en-us_topic_0191813928_li594194191119>`.

   i. .. _alm_19006__en-us_topic_0191813928_aalm-19006_mmccppss_process:

      Rectify the fault by following the steps provided in ALM-19000 HBase Service Unavailable.

   j. Wait several minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.a <alm_19006__en-us_topic_0191813928_li594194191119>`.

#. Check the network connection between RegionServers on active and standby clusters.

   a. .. _alm_19006__en-us_topic_0191813928_li594194191119:

      Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, click the alarm and obtain **HostName** from **Location** in **Alarm Details**.

   c. Log in to the faulty RegionServer node.

   d. Run the **ping** command to check whether the network connection between the faulty RegionServer node and the host where RegionServer of the standby cluster resides is normal.

      -  If yes, go to :ref:`4 <alm_19006__en-us_topic_0191813928_li572522141314>`.
      -  If no, go to :ref:`3.e <alm_19006__en-us_topic_0191813928_s1>`.

   e. .. _alm_19006__en-us_topic_0191813928_s1:

      Contact the O&M personnel to restore the network.

   f. After the network recovers, check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_19006__en-us_topic_0191813928_li572522141314>`.

#. .. _alm_19006__en-us_topic_0191813928_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
