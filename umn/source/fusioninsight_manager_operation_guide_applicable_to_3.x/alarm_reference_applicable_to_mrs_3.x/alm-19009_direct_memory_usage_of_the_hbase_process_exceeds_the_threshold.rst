:original_name: ALM-19009.html

.. _ALM-19009:

ALM-19009 Direct Memory Usage of the HBase Process Exceeds the Threshold
========================================================================

Description
-----------

The system checks the HBase service status every 30 seconds. The alarm is generated when the direct memory usage of an HBase service exceeds the threshold (90% of the maximum memory).

The alarm is cleared when the direct memory usage is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19009    Major          Yes
======== ============== =====================

Parameters
----------

+-------------+------------------------------------------------------------------+
| Name        | Meaning                                                          |
+=============+==================================================================+
| Source      | Specifies the cluster for which the alarm is generated.          |
+-------------+------------------------------------------------------------------+
| ServiceName | Specifies the service name for which the alarm is generated.     |
+-------------+------------------------------------------------------------------+
| RoleName    | Specifies the role name for which the alarm is generated.        |
+-------------+------------------------------------------------------------------+
| HostName    | Specifies the object (host ID) for which the alarm is generated. |
+-------------+------------------------------------------------------------------+

Impact on the System
--------------------

If the available HBase direct memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the HBase service is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check direct memory usage.**

#. On the FusionInsight Manager portal, click **O&M** > **Alarm** > **Alarms** and select the alarm whose **ID** is **19009**. Check the **RoleName** in **Location** and confirm the IP address of **HostName**.

   -  If the role for which the alarm is generated is HMaster, go to :ref:`2 <alm-19009__li51947016195425>`.
   -  If the role for which the alarm is generated is RegionServer, go to :ref:`3 <alm-19009__li17000576195425>`.

#. .. _alm-19009__li51947016195425:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the HMaster for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory** > **HMaster Heap Memory Usage and Direct Memory Usage Statistics** and click **OK** to check whether the used direct memory of the HBase service reaches 90% of the maximum direct memory specified for HBase.

   -  If yes, go to :ref:`4 <alm-19009__li30000576195425>`.
   -  If no, go to :ref:`8 <alm-19009__li62317418195425>`.

#. .. _alm-19009__li17000576195425:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the RegionServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory** > **RegionServer Heap Memory Usage and Direct Memory Usage Statistics** and click **OK** to check whether the used direct memory of the HBase service reaches 90% of the maximum direct memory specified for HBase.

   -  If yes, go to :ref:`4 <alm-19009__li30000576195425>`.
   -  If no, go to :ref:`8 <alm-19009__li62317418195425>`.

#. .. _alm-19009__li30000576195425:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations**, and click **All Configurations**. Choose **HMaster/RegionServer** > **System** and check whether **XX:MaxDirectMemorySize** exists in **GC_OPTS**.

   -  If yes, go to :ref:`5 <alm-19009__li131714294313>`.
   -  If no, go to :ref:`6 <alm-19009__li336333834>`.

#. .. _alm-19009__li131714294313:

   On the FusionInsight Manager portal, choose **Cluster** > *Nameof the desired cluster* > **Services** > **HBase** > **Configurations**, and click **All Configurations**. Choose **HMaster/RegionServer** > **System** and delete **XX:MaxDirectMemorySize** from **GC_OPTS**.

#. .. _alm-19009__li336333834:

   Check whether the **ALM-19008 Heap Memory Usage of the HBase Process Exceeds the Threshold** alarm is generated.

   If yes, handle the alarm by referring to **ALM-19008 Heap Memory Usage of the HBase Process Exceeds the Threshold**.

   If no, go to :ref:`8 <alm-19009__li62317418195425>`.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-19009__li62317418195425>`.

**Collect fault information.**

8.  .. _alm-19009__li62317418195425:

    On the FusionInsight Manager interface of active and standby clusters, choose **O&M** > **Log** > **Download**.

9.  In the **Service** in the required cluster drop-down list box, select **HBase**.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087501.png
