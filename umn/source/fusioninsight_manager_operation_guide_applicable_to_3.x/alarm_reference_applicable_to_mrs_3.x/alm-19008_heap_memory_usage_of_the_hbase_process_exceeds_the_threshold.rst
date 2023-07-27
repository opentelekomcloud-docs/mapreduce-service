:original_name: ALM-19008.html

.. _ALM-19008:

ALM-19008 Heap Memory Usage of the HBase Process Exceeds the Threshold
======================================================================

Description
-----------

The system checks the HBase service status every 30 seconds. The alarm is generated when the heap memory usage of an HBase service exceeds the threshold (90% of the maximum memory).

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19008    Major          Yes
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

If the available HBase heap memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The heap memory of the HBase service is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check heap memory usage.**

#. On the FusionInsight Manager portal, click **O&M** > **Alarm** > **Alarms** and select the alarm whose **ID** is **19008**. Then check the role name in **Location** and confirm the IP adress of the instance.

   -  If the role for which the alarm is generated is HMaster, go to :ref:`2 <alm-19008__li11316139195110>`.
   -  If the role for which the alarm is generated is RegionServer, go to :ref:`3 <alm-19008__li44755158195110>`.

#. .. _alm-19008__li11316139195110:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the HMaster for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory** > **HMaster Heap Memory Usage and Direct Memory Usage Statistics** and click **OK**, check whether the used heap memory of the HBase service reaches 90% of the maximum heap memory specified for HBase.

   -  If yes, go to :ref:`4 <alm-19008__li27009410195110>`.
   -  If no, go to :ref:`6 <alm-19008__li56360562195110>`.

#. .. _alm-19008__li44755158195110:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the RegionServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory** > **RegionServer Heap Memory Usage and Direct Memory Usage Statistics** and click **OK**, check whether the used heap memory of the HBase service reaches 90% of the maximum heap memory specified for HBase.

   -  If yes, go to :ref:`4 <alm-19008__li27009410195110>`.
   -  If no, go to :ref:`6 <alm-19008__li56360562195110>`.

#. .. _alm-19008__li27009410195110:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations**, and click **All Configurations**. Choose **HMaster/RegionServer** > **System**. Increase the value of **-Xmx** in **GC_OPTS** by referring to the Note.

   .. note::

      a. Suggestions on GC parameter configurations for HMaster

         -  Set **-Xms** and **-Xmx** to the same value to prevent JVM from dynamically adjusting the heap memory size and affecting performance.
         -  Set **-XX:NewSize** to the value of **-XX:MaxNewSize**, which is one eighth of **-Xmx**.
         -  For large-scale HBase clusters with a large number of regions, increase values of **GC_OPTS** parameters for HMaster. Specifically, set **-Xmx** to 4 GB if the number of regions is less than 100,000. If the number of regions is more than 100,000, set -Xmx to be greater than or equal to 6 GB. For each increased 35,000 regions, increase the value of **-Xmx** by 2 GB. The maximum value of **-Xmx** is 32 GB.

      b. Suggestions on GC parameter configurations for RegionServer

         -  Set **-Xms** and **-Xmx** to the same value to prevent JVM from dynamically adjusting the heap memory size and affecting performance.
         -  Set **-XX:NewSize** to one eighth of **-Xmx**.
         -  Set the memory for RegionServer to be greater than that for HMaster. If sufficient memory is available, increase the heap memory.
         -  Set **-Xmx** based on the machine memory size. Specifically, set **-Xmx** to 32 GB if the machine memory is greater than 200 GB, to 16 GB if the machine memory is greater than 128 GB and less than 200 GB, and to 8 GB if the machine memory is less than 128 GB. When **-Xmx** is set to 32 GB, a RegionServer node supports 2000 regions and 200 hotspot regions.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-19008__li56360562195110>`.

**Collect fault information.**

6. .. _alm-19008__li56360562195110:

   On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **HBase** in the required cluster from the **Service** drop-down list.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927606.png
