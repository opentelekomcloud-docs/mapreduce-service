:original_name: alm_19000.html

.. _alm_19000:

ALM-19000 HBase Service Unavailable
===================================

Description
-----------

The alarm module checks the HBase service status every 30 seconds. This alarm is generated when the HBase service is unavailable.

This alarm is cleared when the HBase service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19000    Critical       Yes
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

Operations cannot be performed, such as reading or writing data and creating tables.

Possible Causes
---------------

-  ZooKeeper is abnormal.
-  HDFS is abnormal.
-  HBase is abnormal.
-  The network is abnormal.

Procedure
---------

#. Check the ZooKeeper status.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. In the service list, check whether the health status of ZooKeeper is **Good**.

      -  If yes, go to :ref:`2.a <alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_hdfs>`.
      -  If no, go to :ref:`1.c <alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_alm-53004>`.

   c. .. _alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_alm-53004:

      In the alarm list, check whether the alarm ALM-13000 ZooKeeper Service Unavailable exists.

      -  If yes, go to :ref:`1.d <alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_process>`.
      -  If no, go to :ref:`2.a <alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_hdfs>`.

   d. .. _alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_process:

      Rectify the fault by following the steps provided in ALM-13000 ZooKeeper Service Unavailable.

   e. Wait several minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_hdfs>`.

#. Check the HDFS status.

   a. .. _alm_19000__en-us_topic_0191813964_aalm-19000_mmccppss_hdfs:

      On MRS Manager, check whether the ALM-14000 HDFS Service Unavailable alarm is reported.

      -  If yes, go to :ref:`2.b <alm_19000__en-us_topic_0191813964_alm>`.
      -  If no, go to :ref:`3 <alm_19000__en-us_topic_0191813964_li572522141314>`.

   b. .. _alm_19000__en-us_topic_0191813964_alm:

      Rectify the fault by following the steps provided in ALM-14000 HDFS Service Unavailable.

   c. Wait several minutes and check whether the alarm is cleared.

#. .. _alm_19000__en-us_topic_0191813964_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
