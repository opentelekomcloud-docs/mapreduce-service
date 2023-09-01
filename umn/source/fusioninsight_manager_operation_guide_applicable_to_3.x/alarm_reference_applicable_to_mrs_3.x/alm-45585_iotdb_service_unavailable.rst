:original_name: ALM-45585.html

.. _ALM-45585:

ALM-45585 IoTDB Service Unavailable
===================================

Description
-----------

The system checks the IoTDB service status every 300 seconds. This alarm is generated when the IoTDB service is unavailable. This alarm is cleared when the IoTDB service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45585    Critical       Yes
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

Users cannot use the IoTDB service properly.

Possible Causes
---------------

-  The KrbServer service is abnormal.
-  More than 50% of IoTDBServer instances are faulty.

Procedure
---------

**Check whether the KrbServer service on which the IoTDB depends is abnormal.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether ALM-25500 KrbServer Service Unavailable exists.

   -  If yes, go to :ref:`3 <alm-45585__li1857611153310>`.
   -  If no, go to :ref:`5 <alm-45585__li1336018269214>`.

#. .. _alm-45585__li1857611153310:

   Handle the alarm by referring to "ALM-25500 KrbServer Service Unavailable."

#. After ALM-25500 is cleared, wait a few minutes and check whether the alarm HetuServer Service Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45585__li1336018269214>`.

**Check whether IoTDBServer instances are faulty.**

5. .. _alm-45585__li1336018269214:

   On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **IoTDB** > **Instance**.

6. Check whether the percentage of faulty IoTDBServer instances exceeds 50%. If yes, restart the faulty IoTDBServer instances and check whether the status is restored.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45585__li4749473185459>`.

**Collect the fault information.**

7.  .. _alm-45585__li4749473185459:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, select **IoTDB** for the target cluster, and click **OK**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927517.png
