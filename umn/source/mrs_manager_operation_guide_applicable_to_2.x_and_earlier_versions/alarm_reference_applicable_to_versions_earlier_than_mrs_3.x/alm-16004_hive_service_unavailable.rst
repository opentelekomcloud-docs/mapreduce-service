:original_name: alm_16004.html

.. _alm_16004:

ALM-16004 Hive Service Unavailable
==================================

Description
-----------

The system checks the Hive service status every 30 seconds. This alarm is generated when the Hive service is unavailable.

This alarm is cleared when the Hive service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16004    Critical       Yes
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

The system cannot provide data loading, query, and extraction services.

Possible Causes
---------------

-  Basic services, such as ZooKeeper, HDFS, Yarn, and DBService work incorrectly, or the Hive process is faulty.

   -  ZooKeeper is abnormal.
   -  HDFS is abnormal.
   -  Yarn is abnormal.
   -  DBService is abnormal.
   -  The Hive service process is faulty. If the alarm is caused by a Hive process fault, the alarm report has a delay of about 5 minutes.

-  The network communication between the Hive service and basic services is interrupted.

Procedure
---------

#. Check the HiveServer/MetaStore process status.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **Hive** > **Instances**. In the Hive instance list, check whether the status of all HiveSserver/MetaStore instances is **Unknown**.

      -  If yes, go to :ref:`1.c <alm_16004__en-us_topic_0191813910_li15736882153452>`.
      -  If no, go to :ref:`2 <alm_16004__en-us_topic_0191813910_li63276134153458>`.

   c. .. _alm_16004__en-us_topic_0191813910_li15736882153452:

      Above the Hive instance list, choose **More** > **Restart Instance** to restart the HiveServer/MetaStore process.

   d. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_16004__en-us_topic_0191813910_li63276134153458>`.

#. .. _alm_16004__en-us_topic_0191813910_li63276134153458:

   Check the ZooKeeper status.

   a. Go to the cluster details page and choose **Alarms**.

   b. On MRS Manager, check whether the ALM-12007 Process Fault alarm is reported.

      -  If yes, go to :ref:`2.c <alm_16004__en-us_topic_0191813910_li17867059153452>`.
      -  If no, go to :ref:`3 <alm_16004__en-us_topic_0191813910_li315441715352>`.

   c. .. _alm_16004__en-us_topic_0191813910_li17867059153452:

      In the **Alarm Details** area of ALM-12007 Process Fault, check whether **ServiceName** is **ZooKeeper**.

      -  If yes, go to :ref:`2.d <alm_16004__en-us_topic_0191813910_li26585804153452>`.
      -  If no, go to :ref:`3 <alm_16004__en-us_topic_0191813910_li315441715352>`.

   d. .. _alm_16004__en-us_topic_0191813910_li26585804153452:

      Rectify the fault by following steps provided in ALM-12007 Process Fault.

   e. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_16004__en-us_topic_0191813910_li315441715352>`.

#. .. _alm_16004__en-us_topic_0191813910_li315441715352:

   Check the HDFS status.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, check whether the alarm ALM-14000 HDFS Service Unavailable exists.

      -  If yes, go to :ref:`3.c <alm_16004__en-us_topic_0191813910_li2196200153452>`.
      -  If no, go to :ref:`4 <alm_16004__en-us_topic_0191813910_li3789476315357>`.

   c. .. _alm_16004__en-us_topic_0191813910_li2196200153452:

      Rectify the fault by following the steps provided in ALM-14000 HDFS Service Unavailable.

   d. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_16004__en-us_topic_0191813910_li3789476315357>`.

#. .. _alm_16004__en-us_topic_0191813910_li3789476315357:

   Check the Yarn status.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list on MRS Manager, check whether the alarm ALM-18000 Yarn Service Unavailable is generated.

      -  If yes, go to :ref:`4.c <alm_16004__en-us_topic_0191813910_li64260695153452>`.
      -  If no, go to :ref:`4 <alm_16004__en-us_topic_0191813910_li3789476315357>`.

   c. .. _alm_16004__en-us_topic_0191813910_li64260695153452:

      Rectify the fault by following the steps provided in ALM-18000 Yarn Service Unavailable.

   d. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_16004__en-us_topic_0191813910_li3789476315357>`.

#. Check the DBService status.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list on MRS Manager, check whether ALM-27001 DBService Unavailable is generated.

      -  If yes, go to :ref:`5.c <alm_16004__en-us_topic_0191813910_li19704975153452>`.
      -  If no, go to :ref:`6 <alm_16004__en-us_topic_0191813910_li23165657153517>`.

   c. .. _alm_16004__en-us_topic_0191813910_li19704975153452:

      Rectify the fault by following the handling procedure in :ref:`ALM-27001 DBService Is Unavailable <alm_27001>`.

   d. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`6 <alm_16004__en-us_topic_0191813910_li23165657153517>`.

#. .. _alm_16004__en-us_topic_0191813910_li23165657153517:

   Check the network connection between Hive and ZooKeeper, HDFS, Yarn, and DBService.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Click **Hive**.

   c. Click **Instances**.

      The HiveServer instance list is displayed.

   d. Click **Host Name** in the row of **HiveServer**.

      The HiveServer host status page is displayed.

   e. .. _alm_16004__en-us_topic_0191813910_li39788839153452:

      Record the IP address under **Summary**.

   f. Use the IP address obtained in :ref:`6.e <alm_16004__en-us_topic_0191813910_li39788839153452>` to log in to the host where HiveServer is located.

   g. Run the **ping** command to check whether the network connection between the host that runs HiveServer and the hosts that run the ZooKeeper, HDFS, Yarn, and DBService services is normal. Methods of obtaining IP addresses of the hosts that run ZooKeeper, HDFS, Yarn, and DBService services as well as the HiveServer IP address are the same.

      -  If yes, go to :ref:`7 <alm_16004__en-us_topic_0191813910_li572522141314>`.
      -  If no, go to :ref:`6.h <alm_16004__en-us_topic_0191813910_li44761520153452>`.

   h. .. _alm_16004__en-us_topic_0191813910_li44761520153452:

      Contact the O&M personnel to restore the network.

   i. In the alarm list, check whether ALM-16004 Hive Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`7 <alm_16004__en-us_topic_0191813910_li572522141314>`.

#. .. _alm_16004__en-us_topic_0191813910_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
