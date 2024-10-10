:original_name: ALM-45736.html

.. _ALM-45736:

ALM-45736 Guardian Service Unavailable
======================================

Alarm Description
-----------------

The alarm module checks the Guardian service status every 60 seconds. This alarm is generated if Guardian is unavailable.

This alarm is cleared after Guardian recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45736    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

=========== ========================================================
Parameter   Description
=========== ========================================================
Source      Specifies the cluster for which the alarm was generated.
ServiceName Specifies the service for which the alarm was generated.
RoleName    Specifies the role for which the alarm was generated.
HostName    Specifies the host for which the alarm was generated.
=========== ========================================================

Impact on the System
--------------------

Guardian cannot work properly.

Possible Causes
---------------

-  The HDFS service on which the Guardian service depends is abnormal.
-  The TokenServer role instance is abnormal.

Handling Procedure
------------------

**Check the HDFS service status.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, check whether "ALM-14000 HDFS Service Unavailable" is reported.

   -  If yes, go to :ref:`2 <alm-45736__l0ca5fe03ce10420c9ad6c90f8583a4bd>`.
   -  If no, go to :ref:`3 <alm-45736__li43869374161349>`.

#. .. _alm-45736__l0ca5fe03ce10420c9ad6c90f8583a4bd:

   Clear this alarm according to the alarm help.

   After the alarm is cleared, wait a few minutes and check whether the alarm GuardianService Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-45736__li43869374161349>`.

**Check all TokenServer instances.**

3. .. _alm-45736__li43869374161349:

   Log in to the node where the TokenServer instance resides as user **omm** and run the **ps -ef|grep "guardian.token.server.Server"** command to check whether the TokenServer process exists on the node.

   -  If yes, go to :ref:`5 <alm-45736__li16749195915615>`.
   -  If no, restart the faulty TokenServer instance and go to :ref:`4 <alm-45736__li60791811161349>`.

4. .. _alm-45736__li60791811161349:

   In the alarm list, check whether the alarm "Guardian Service Unavailable" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45736__li16749195915615>`.

**Collect fault information.**

5. .. _alm-45736__li16749195915615:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Guardian** for the destination cluster.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002008102449.png
