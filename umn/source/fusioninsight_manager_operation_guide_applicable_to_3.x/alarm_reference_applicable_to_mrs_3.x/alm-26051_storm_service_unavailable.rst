:original_name: ALM-26051.html

.. _ALM-26051:

ALM-26051 Storm Service Unavailable
===================================

Description
-----------

The system checks the Storm service status every 30 seconds. This alarm is generated when all Nimbus nodes in the cluster are abnormal and the Storm service is unavailable.

This alarm is cleared when the Storm service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
26051    Critical       Yes
======== ============== =====================

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

The cluster cannot provide the Storm service, and users cannot perform new Storm tasks.

Possible Causes
---------------

-  The Kerberos cluster is faulty.
-  The ZooKeeper cluster is faulty or suspended.
-  The active and standby Nimbus nodes in the Storm cluster are abnormal

Procedure
---------

**Check the status of the Kerberos cluster. (Skip this step if the normal mode is used.)**

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Check whether the running status of the Kerberos service is **Normal**.

   -  If yes, go to :ref:`5 <alm-26051__li48640467201537>`.
   -  If no, go to :ref:`3 <alm-26051__li46537612201537>`.

#. .. _alm-26051__li46537612201537:

   See the related maintenance information of **ALM-25500 KrbServer Service Unavailable**.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-26051__li48640467201537>`.

**Check the status of the ZooKeeper cluster.**

5. .. _alm-26051__li48640467201537:

   Check whether the running status of the ZooKeeper service is **Normal**.

   -  If yes, go to :ref:`8 <alm-26051__li55312065201537>`.
   -  If no, go to :ref:`6 <alm-26051__li47563765201537>`.

6. .. _alm-26051__li47563765201537:

   If ZooKeeper service is stopped, start it, else see the related maintenance information of **ALM-13000 ZooKeeper Service Unavailable**.

7. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-26051__li55312065201537>`.

**Check the status of the active and standby Nimbus nodes.**

8.  .. _alm-26051__li55312065201537:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **Storm** > **Nimbus** to go to the Nimbus Instances page.

9.  Check whether only one Nimbus node that is in the **Active** state in **Roles**.

    -  If yes, go to :ref:`13 <alm-26051__li7146378201537>`.
    -  If no, go to :ref:`10 <alm-26051__li27079930201537>`.

10. .. _alm-26051__li27079930201537:

    Select two Nimbus role instances, choose **More** > **Restart Instance**, and check whether the instances restart successfully.

    -  If yes, go to :ref:`11 <alm-26051__li54175710201537>`.
    -  If no, go to :ref:`13 <alm-26051__li7146378201537>`.

11. .. _alm-26051__li54175710201537:

    Log in to the FusionInsight Manager portal again, choose **Cluster** > *Name of the desired cluster* > **Services** > **Storm** > **Nimbus** to check whether the running status is **Normal**.

    -  If yes, go to :ref:`12 <alm-26051__li14738771201537>`.
    -  If no, go to :ref:`13 <alm-26051__li7146378201537>`.

12. .. _alm-26051__li14738771201537:

    Wait for 30 seconds and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-26051__li7146378201537>`.

**Collecting Fault Information**

13. .. _alm-26051__li7146378201537:

    On the FusionInsight Manager, choose **O&M** > **Log** > **Download**.

14. Select the following nodes in the required cluster from the **Service** drop-down list:

    -  KrbServer

       .. note::

          KrbServer logs do not need to be downloaded in normal mode.

    -  ZooKeeper
    -  Storm

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417460.png
