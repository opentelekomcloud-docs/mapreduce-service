:original_name: ALM-45275.html

.. _ALM-45275:

ALM-45275 Ranger Service Unavailable
====================================

Description
-----------

The alarm module checks the Ranger service status every 180 seconds. This alarm is generated if the Ranger service is abnormal.

This alarm is cleared after the Ranger service recovers.

Attributes
----------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
45275    Critical       Yes
======== ============== =====================

Parameters
----------

=========== =========================================
Name        Meaning
=========== =========================================
Source      Cluster for which the alarm is generated.
ServiceName Service for which the alarm is generated.
RoleName    Role for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =========================================

Impact on the System
--------------------

When the Ranger service is unavailable, Ranger cannot work properly and the native Ranger UI cannot be accessed.

Possible Causes
---------------

-  The DBService service on which Ranger depends is abnormal.
-  The RangerAdmin role instance is abnormal.

Procedure
---------

**Check the DBService process status.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the displayed page, check whether the ALM-27001 DBService Service Unavailable alarm is reported.

   -  If yes, go to :ref:`2 <alm-45275__li24833719161349>`.
   -  If no, go to :ref:`3 <alm-45275__li43869374161349>`.

#. .. _alm-45275__li24833719161349:

   Rectify the DBService service fault by following the handling procedure of ALM-27001 DBService Service Unavailable. After the DBService alarm is cleared, check whether Ranger Service Unavailable alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-45275__li43869374161349>`.

**Check all RangerAdmin instances.**

3. .. _alm-45275__li43869374161349:

   Log in to the node where the RangerAdmin instance is located as user **omm** and run the **ps -ef|grep "proc_rangeradmin"** command to check whether the RangerAdmin process exists on the current node.

   -  If yes, go to :ref:`5 <alm-45275__li16749195915615>`.
   -  If no, restart the faulty RangerAdmin instance or Ranger service and go to :ref:`4 <alm-45275__li60791811161349>`.

4. .. _alm-45275__li60791811161349:

   In the alarm list, check whether the alarm "Ranger Service Unavailable" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45275__li16749195915615>`.

**Collect the fault information.**

5. .. _alm-45275__li16749195915615:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Ranger** for the target cluster.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault that triggers the alarm is rectified, the alarm is automatically cleared.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767366.png
