:original_name: ALM-43001.html

.. _ALM-43001:

ALM-43001 Spark2x Service Unavailable
=====================================

Description
-----------

The system checks the Spark2x service status every 300 seconds. This alarm is generated when the Spark2x service is unavailable.

This alarm is cleared when the Spark2x service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
43001    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
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
-  HDFS is abnormal.
-  Yarn is abnormal.
-  The corresponding Hive service is abnormal.
-  The Spark2x assembly package is abnormal.

Procedure
---------

If the alarm is abnormal Spark2x assembly packet, the Spark packet is abnormal. Wait for about 10 minutes. The alarm is automatically cleared.

**Check whether service unavailability alarms exist in services that Spark2x depends on.**

#. On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**.

#. Check whether the following alarms exist in the alarm list:

   -  ALM-25500 KrbServer Service Unavailable
   -  ALM-25000 LdapServer Service Unavailable
   -  ALM-13000 ZooKeeper Service Unavailable
   -  ALM-14000 HDFS Service Unavailable
   -  ALM-18000 Yarn Service Unavailable
   -  ALM-16004 Hive Service Unavailable

   .. note::

      If the multi-instance function is enabled for the cluster and multiple Spark2x services are installed, check the Spark2x service for which the alarm is generated based on the value of **ServiceName** in location information and check whether the Hive service is faulty. Spark2x corresponds to Hive, spark2x1 corresponds to Hive1, and other services follow the same rule.

   -  If yes, go to :ref:`3 <alm-43001__l0ca5fe03ce10420c9ad6c90f8583a4bd>`.
   -  If no, go to :ref:`4 <alm-43001__en-us_topic_0085589435_li3748337517>`.

#. .. _alm-43001__l0ca5fe03ce10420c9ad6c90f8583a4bd:

   Handle the alarms based on the troubleshooting methods provided in the alarm help.

   After the alarm is cleared, wait a few minutes and check whether the alarm GuardianService Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-43001__en-us_topic_0085589435_li3748337517>`.

**Collect fault information.**

4. .. _alm-43001__en-us_topic_0085589435_li3748337517:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

5. In the **Service** area, select the following nodes of the desired cluster. (Hive is the specific Hive service determined based on **ServiceName** in the alarm location information).

   -  KrbServer
   -  LdapServer
   -  ZooKeeper
   -  HDFS
   -  Yarn
   -  Hive

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895574.png
