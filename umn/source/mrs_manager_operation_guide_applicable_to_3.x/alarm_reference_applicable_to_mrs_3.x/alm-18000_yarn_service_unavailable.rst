:original_name: ALM-18000.html

.. _ALM-18000:

ALM-18000 Yarn Service Unavailable
==================================

Description
-----------

This alarm is generated when the Yarn service is unavailable. The alarm module checks the Yarn service status every 60 seconds.

The alarm is cleared when the Yarn service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18000    Critical       Yes
======== ============== =====================

Parameters
----------

========== =======================================================
Name       Meaning
========== =======================================================
Source     Specifies the cluster for which the alarm is generated.
ServiceNam Specifies the service for which the alarm is generated.
RoleName   Specifies the role for which the alarm is generated.
HostName   Specifies the host for which the alarm is generated.
========== =======================================================

Impact on the System
--------------------

The cluster cannot provide Yarn services. Users cannot run new applications. Submitted applications cannot be run.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  The HDFS service is abnormal.
-  There is no active ResourceManager instance in the Yarn cluster.
-  All the NodeManagers in the Yarn cluster are abnormal.

Procedure
---------

**Check ZooKeeper service status.**

#. On the MRS Manager, check whether the alarm list contains **ALM-13000 ZooKeeper Service Unavailable**.

   -  If yes, go to :ref:`2 <alm-18000__li311182174725>`.
   -  If no, go to :ref:`3 <alm-18000__li19148237174725>`.

#. .. _alm-18000__li311182174725:

   Rectify the fault by following the steps provided in **ALM-13000 ZooKeeper Service Unavailable**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-18000__li19148237174725>`.

**Check the HDFS service status.**

3. .. _alm-18000__li19148237174725:

   On the MRS Manager, check whether the alarm list contains the HDFS alarms.

   -  If yes, go to :ref:`4 <alm-18000__li13219687174725>`.
   -  If no, go to :ref:`5 <alm-18000__li40584762174725>`.

4. .. _alm-18000__li13219687174725:

   Choose **O&M > Alarm > Alarms**, handle HDFS alarms based on the alarm help, and check whether the Yarn alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18000__li40584762174725>`.

**Check the ResourceManager status in the Yarn cluster.**

5. .. _alm-18000__li40584762174725:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Yarn**.

6. In **Dashboard**, check whether there is an active ResourceManager instance in the Yarn cluster.

   -  If yes, go to :ref:`7 <alm-18000__li7454663174725>`.
   -  If no, go to :ref:`10 <alm-18000__li46526163174725>`.

**Check the NodeManager node status in the Yarn cluster.**

7. .. _alm-18000__li7454663174725:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Yarn** > **Instance**.

8. Query NodeManager **Running Status**, and check whether there are unhealthy nodes.

   -  If yes, go to :ref:`9 <alm-18000__li25011012174725>`.
   -  If no, go to :ref:`10 <alm-18000__li46526163174725>`.

9. .. _alm-18000__li25011012174725:

   Rectify the fault by following the steps provided in **ALM-18002 NodeManager Heartbeat Lost** or **ALM-18003 NodeManager Unhealthy**. After the fault is rectified, check whether the Yarn alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-18000__li46526163174725>`.

**Collect fault information.**

10. .. _alm-18000__li46526163174725:

    On the MRS Manager portal of the active cluster, choose **O&M** > **Log > Download**.

11. Select **Yarn** in the required cluster from the **Service**.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127409.png
