:original_name: ALM-45615.html

.. _ALM-45615:

ALM-45615 CDL Service Unavailable
=================================

Description
-----------

The system checks the CDL health status every 60 seconds. This alarm is generated when the CDL health status is **DOWN**. This alarm is cleared when the system detects that the CDL health status is **UP**.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45615    Critical       Yes
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

The CDL service is abnormal. You cannot use FusionInsight Manager to perform cluster operations on the CDL service. The CDL service function is unavailable.

Possible Causes
---------------

All CDLService or CDLConnector instances of the CDL service are abnormal, and the Kafka service is unavailable.

Procedure
---------

**Check whether the Kafka service on which the CDL service depends is abnormal.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether ALM-38000 Kafka Service Unavailable exists.

   -  If yes, go to :ref:`3 <alm-45615__li1857611153310>`.
   -  If no, go to :ref:`5 <alm-45615__li1336018269214>`.

#. .. _alm-45615__li1857611153310:

   Handle the alarm by referring to "ALM-38000 Kafka Service Unavailable".

#. After the alarm is cleared, wait a few minutes and check whether the alarm HetuServer Service Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45615__li1336018269214>`.

**Check whether CDL instances are faulty.**

5. .. _alm-45615__li1336018269214:

   On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **CDL** > **Instance**.

6. Check whether all CDLService and CDLConnector instances are faulty.

   -  If yes, restart the CDL service and choose **Cluster** > *Name of the desired cluster* > **Services** > **CDL** > **More** > **Restart Service**. If the fault persists after the restart, go to :ref:`7 <alm-45615__li4749473185459>` and contact O&M personnel to check CDL logs.
   -  If no, go to :ref:`7 <alm-45615__li4749473185459>`.

**Collect the fault information.**

7.  .. _alm-45615__li4749473185459:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **CDL** for the target cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the service is restored, the system automatically clears the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767706.png
