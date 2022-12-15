:original_name: alm_14000.html

.. _alm_14000:

ALM-14000 HDFS Service Unavailable
==================================

Description
-----------

The system checks the service status of NameService every 30 seconds. This alarm is generated when the system considers that the HDFS service is unavailable because all the NameService services are abnormal.

This alarm is cleared when at least one NameService service is normal and the system considers that the HDFS service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14000    Critical       Yes
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

HDFS fails to provide services for HDFS service-based upper-layer components, such as HBase and MapReduce. As a result, users cannot read or write files.

Possible Causes
---------------

-  ZooKeeper is abnormal.
-  All NameService services are abnormal.

Procedure
---------

#. Check the ZooKeeper status.

   a. Go to the MRS cluster details page. On the **Components** tab page, check whether the health status of the ZooKeeper service is **Good**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click the **Services** tab.

      -  If yes, go to :ref:`1.b <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss2>`.
      -  If no, go to :ref:`2.a <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss4>`.

   b. .. _alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss2:

      Rectify the health status of the ZooKeeper service. For details, see :ref:`ALM-13000 ZooKeeper Service Unavailable <alm_13000>`. Then check whether the health status of the ZooKeeper service is **Good**.

      -  If yes, go to :ref:`1.c <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss3>`.
      -  If no, go to :ref:`3 <alm_14000__en-us_topic_0191813870_li572522141314>`.

   c. .. _alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss3:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss4>`.

#. Handle the NameService service exception alarm.

   a. .. _alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss4:

      Go to the MRS cluster details page. On the **Alarms** page, check whether all NameService services have abnormal alarms.

      -  If yes, go to :ref:`2.b <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss5>`.
      -  If no, go to :ref:`3 <alm_14000__en-us_topic_0191813870_li572522141314>`.

   b. .. _alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_ss5:

      Handle the abnormal NameService services following the instructions in :ref:`ALM-14010 NameService Service Is Abnormal <alm_14010>` and check whether each NameService service exception alarm is cleared.

      -  If yes, go to :ref:`2.c <alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_checkbk_5>`.
      -  If no, go to :ref:`3 <alm_14000__en-us_topic_0191813870_li572522141314>`.

   c. .. _alm_14000__en-us_topic_0191813870_cn_58_42_000001_4_mmccppss_checkbk_5:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_14000__en-us_topic_0191813870_li572522141314>`.

#. .. _alm_14000__en-us_topic_0191813870_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
