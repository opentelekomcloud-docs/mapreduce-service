:original_name: ALM-24000.html

.. _ALM-24000:

ALM-24000 Flume Service Unavailable
===================================

Description
-----------

The alarm module checks the Flume service status every 180 seconds. This alarm is generated if the Flume service is abnormal.

This alarm is automatically cleared after the Flume service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24000    Critical       Yes
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

Flume cannot work and data transmission is interrupted.

Possible Causes
---------------

All Flume instances are faulty.

Procedure
---------

#. Log in to a Flume node as user **omm** and run the **ps -ef|grep "flume.role=server"** command to check whether the Flume process exists on the node.

   -  If yes, go to :ref:`3 <alm-24000__li22384958105055>`.
   -  If no, restart the faulty Flume node or Flume service and go to :ref:`2 <alm-24000__li62139541105055>`.

#. .. _alm-24000__li62139541105055:

   In the alarm list, check whether alarm "Flume Service Unavailable" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-24000__li22384958105055>`.

**Collect the fault information.**

3. .. _alm-24000__li22384958105055:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

4. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

5. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

6. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767398.png
