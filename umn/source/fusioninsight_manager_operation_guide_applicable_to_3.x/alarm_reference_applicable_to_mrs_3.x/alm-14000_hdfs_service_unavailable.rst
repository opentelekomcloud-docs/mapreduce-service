:original_name: ALM-14000.html

.. _ALM-14000:

ALM-14000 HDFS Service Unavailable
==================================

Description
-----------

The system checks the NameService service status every 60 seconds. This alarm is generated when all the NameService services are abnormal and the system considers that the HDFS service is unavailable.

This alarm is cleared when at least one NameService service is normal and the system considers that the HDFS service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14000    Critical       Yes
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

HDFS fails to provide services for HDFS service-based upper-layer components, such as HBase and MapReduce. As a result, users cannot read or write files.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  All NameService services are abnormal.

Procedure
---------

**Check the ZooKeeper service status.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms**. On the Alarm page, check whether **ALM-13000 ZooKeeper Service Unavailable** is reported.

   -  If yes, go to :ref:`2 <alm-14000__li31253013162114>`.
   -  If no, go to :ref:`4 <alm-14000__li57039289162114>`.

#. .. _alm-14000__li31253013162114:

   See **ALM-13000 ZooKeeper Service Unavailable** to rectify the health status of ZooKeeper fault and check whether the **Running** **Status** of the ZooKeeper service restores to **Normal**.

   -  If yes, go to :ref:`3 <alm-14000__li19570784162114>`.
   -  If no, go to :ref:`7 <alm-14000__li44697640162114>`.

#. .. _alm-14000__li19570784162114:

   On the **O&M > Alarm > Alarms** page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14000__li57039289162114>`.

**Handle the NameService service exception alarm.**

4. .. _alm-14000__li57039289162114:

   On the FusionInsight Manager portal, choose **O&M > Alarm** **> Alarms**. On the Alarms page, check whether **ALM-14010 NameService Service Unavailable** is reported.

   -  If yes, go to :ref:`5 <alm-14000__li25596313162114>`.
   -  If no, go to :ref:`7 <alm-14000__li44697640162114>`.

5. .. _alm-14000__li25596313162114:

   See **ALM-14010 NameService Service Unavailable** to handle the abnormal NameService services and check whether each NameService service exception alarm is cleared.

   -  If yes, go to :ref:`6 <alm-14000__li7149629162114>`.
   -  If no, go to :ref:`7 <alm-14000__li44697640162114>`.

6. .. _alm-14000__li7149629162114:

   On the **O&M > Alarm > Alarms** page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-14000__li44697640162114>`.

**Collect fault information.**

7.  .. _alm-14000__li44697640162114:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select the following nodes in the required cluster from the **Service**:

    -  ZooKeeper
    -  HDFS

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383957.png
