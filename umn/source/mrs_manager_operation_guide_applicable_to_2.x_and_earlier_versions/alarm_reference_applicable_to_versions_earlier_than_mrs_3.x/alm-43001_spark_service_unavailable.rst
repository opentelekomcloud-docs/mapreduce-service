:original_name: alm_43001.html

.. _alm_43001:

ALM-43001 Spark Service Unavailable
===================================

Description
-----------

The system checks the Spark service status every 60 seconds. This alarm is generated when the Spark service is unavailable.

This alarm is cleared when the Spark service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
43001    Critical       Yes
======== ============== =====================

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

The Spark tasks submitted by users fail to be executed.

Possible Causes
---------------

-  The KrbServer service is abnormal.
-  The LdapServer service is abnormal.
-  ZooKeeper is abnormal.
-  The HDFS service is abnormal.
-  The Yarn service is abnormal.
-  The corresponding Hive service is abnormal.

Procedure
---------

#. Check whether service unavailability alarms exist in services that Spark depends on.

   a. Go to the cluster details page and choose **Alarms**.

   b. Check whether the following alarms exist in the alarm list:

      #. ALM-25500 KrbServer Service Unavailable
      #. ALM-25000 LdapServer Service Unavailable
      #. ALM-13000 ZooKeeper Service Unavailable
      #. ALM-14000 HDFS Service Unavailable
      #. ALM-18000 Yarn Service Unavailable
      #. ALM-16004 Hive Service Unavailable

      -  If yes, go to :ref:`1.c <alm_43001__en-us_topic_0191813893_li1257801171836>`.
      -  If no, go to :ref:`2 <alm_43001__en-us_topic_0191813893_li572522141314>`.

   c. .. _alm_43001__en-us_topic_0191813893_li1257801171836:

      Handle the alarm according to the alarm help.

      After the alarm is cleared, wait a few minutes and check whether the alarm HetuServer Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_43001__en-us_topic_0191813893_li572522141314>`.

#. .. _alm_43001__en-us_topic_0191813893_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
