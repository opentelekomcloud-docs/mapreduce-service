:original_name: ALM-18021.html

.. _ALM-18021:

ALM-18021 Mapreduce Service Unavailable
=======================================

Description
-----------

The alarm module checks the MapReduce service status every 60 seconds. This alarm is generated when the system detects that the MapReduce service is unavailable.

The alarm is cleared when the MapReduce service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18021    Critical       Yes
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

The cluster cannot provide the MapReduce service. For example, MapReduce cannot be used to view task logs or the log archive function is unavailable.

Possible Causes
---------------

-  The JobHistoryServer instance is abnormal.
-  The KrbServer service is abnormal.
-  The ZooKeeper service abnormal.
-  The HDFS service abnormal.
-  The Yarn service is abnormal.

Procedure
---------

**Check** **MapReduce service JobHistoryServer instance status.**

#. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **MapReduce** > **Instance**.
#. Check whether the running status of JobHistoryServer is **Normal**.

   -  If yes, go to :ref:`11 <alm-18021__li795116716116>`.
   -  If no, go to :ref:`3 <alm-18021__li2896399895811>`.

**Check the KrbServer service status.**

3. .. _alm-18021__li2896399895811:

   In the alarm list on FusionInsight Manager, check whether **ALM-25500 KrbServer Service Unavailable** exists.

   -  If yes, go to :ref:`4 <alm-18021__li6544511395811>`.
   -  If no, go to :ref:`5 <alm-18021__li4793762895811>`.

4. .. _alm-18021__li6544511395811:

   Rectify the fault by following the steps provided in **ALM-25500 KrbServer Service Unavailable**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18021__li4793762895811>`.

**Check the ZooKeeper service.**

5. .. _alm-18021__li4793762895811:

   In the alarm list on FusionInsight Manager, check whether **ALM-13000 ZooKeeper Service Unavailable** exists.

   -  If yes, go to :ref:`6 <alm-18021__li4474654695811>`.
   -  If no, go to :ref:`7 <alm-18021__li247717695811>`.

6. .. _alm-18021__li4474654695811:

   Rectify the fault by following the steps provided in **ALM-13000 ZooKeeper Service Unavailable**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18021__li247717695811>`.

**Check the HDFS service status.**

7. .. _alm-18021__li247717695811:

   In the alarm list on FusionInsight Manager, check whether **ALM-14000 HDFS Service Unavailable** exists.

   -  If yes, go to :ref:`8 <alm-18021__li5261529695811>`.
   -  If no, go to :ref:`9 <alm-18021__li19148237174725>`.

8. .. _alm-18021__li5261529695811:

   Rectify the fault by following the steps provided in **ALM-14000 HDFS Service Unavailable**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-18021__li19148237174725>`.

**Check the Yarn service status.**

9.  .. _alm-18021__li19148237174725:

    In the alarm list on FusionInsight Manager, check whether **ALM-18000 Yarn Service Unavailable** exists.

    -  If yes, go to :ref:`10 <alm-18021__li13219687174725>`
    -  If no, go to :ref:`11 <alm-18021__li795116716116>`.

10. .. _alm-18021__li13219687174725:

    Rectify the fault by following the steps provided in **ALM-18000 Yarn Service Unavailable**, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-18021__li795116716116>`.

**Collect fault information.**

11. .. _alm-18021__li795116716116:

    On the FusionInsight Manager home page of the active cluster, choose **O&M** > **Log > Download.**

12. Select **MapReduce** in the required cluster from the **Service.**

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807805.png
