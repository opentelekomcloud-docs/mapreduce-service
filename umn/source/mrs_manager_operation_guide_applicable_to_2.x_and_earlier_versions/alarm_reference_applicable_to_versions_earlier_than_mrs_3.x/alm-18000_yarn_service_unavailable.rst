:original_name: alm_18000.html

.. _alm_18000:

ALM-18000 Yarn Service Unavailable
==================================

Description
-----------

The alarm module checks the Yarn service status every 30 seconds. This alarm is generated when the Yarn service is unavailable.

This alarm is cleared when the Yarn service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18000    Critical       Yes
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

The cluster cannot provide the Yarn service. Users cannot run new applications. Submitted applications cannot be run.

Possible Causes
---------------

-  ZooKeeper is abnormal.
-  HDFS is abnormal.
-  There is no active ResourceManager node in the Yarn cluster.
-  All NodeManager nodes in the Yarn cluster are abnormal.

Procedure
---------

#. Check the ZooKeeper status.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, check whether the alarm ALM-13000 ZooKeeper Service Unavailable exists.

      -  If yes, go to :ref:`1.c <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss2>`.
      -  If no, go to :ref:`2.b <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss3>`.

   c. .. _alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss2:

      Rectify the fault by following the handling procedure in :ref:`ALM-13000 ZooKeeper Service Unavailable <alm_13000>`. Then, check whether this alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.b <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss3>`.

#. Check the HDFS status.

   a. Go to the cluster details page and choose **Alarms**.

   b. .. _alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss3:

      In the alarm list, check whether an HDFS alarm is generated.

      -  If yes, go to :ref:`2.c <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss4>`.
      -  If no, go to :ref:`3.b <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss5>`.

   c. .. _alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss4:

      Click **Alarms**, and handle HDFS alarms according to **Alarm Help**. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.b <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss5>`.

#. Check the ResorceManager status in the Yarn cluster.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_ss5:

      Click **Yarn**.

   c. In **Yarn Summary**, check whether there is an active ResourceManager node in the Yarn cluster.

      -  If yes, go to :ref:`4.b <alm_18000__en-us_topic_0191813947_step_5>`.
      -  If no, go to :ref:`5 <alm_18000__en-us_topic_0191813947_li572522141314>`.

#. Check the NodeManager node status in the Yarn cluster.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_18000__en-us_topic_0191813947_step_5:

      Choose **Yarn** > **Instances**.

   c. Check **Health Status** of NodeManager, and check whether there are unhealthy nodes.

      -  If yes, go to :ref:`4.d <alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_step_7>`.
      -  If no, go to :ref:`5 <alm_18000__en-us_topic_0191813947_li572522141314>`.

   d. .. _alm_18000__en-us_topic_0191813947_aalm-18000_mmccppss_step_7:

      Rectify the fault by following the procedure provided in :ref:`ALM-18002 NodeManager Heartbeat Lost <alm_18002>` or :ref:`ALM-18003 NodeManager Unhealthy <alm_18003>`. Then, check whether this alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm_18000__en-us_topic_0191813947_li572522141314>`.

#. .. _alm_18000__en-us_topic_0191813947_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
