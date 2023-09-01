:original_name: ALM-19007.html

.. _ALM-19007:

ALM-19007 HBase GC Time Exceeds the Threshold
=============================================

Description
-----------

The system checks the old generation garbage collection (GC) time of the HBase service every 60 seconds. This alarm is generated when the detected old generation GC time exceeds the threshold (exceeds 5 seconds for three consecutive checks by default). To change the threshold, on the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HBase > GC >** **GC time for old generation**. This alarm is cleared when the old generation GC time of the HBase service is shorter than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19007    Major          Yes
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

If the old generation GC time exceeds the threshold, HBase data read and write are affected.

Possible Causes
---------------

The memory of HBase instances is overused, the heap memory is inappropriately allocated, or a large number of I/O operations exist in HBase. As a result, GCs occur frequently.

Procedure
---------

**Check the GC time.**

#. On the FusionInsight Manager portal, click **O&M** > **Alarm** > **Alarms** and select the alarm whose **ID** is **19007**. Then check the role name in **Location** and confirm the IP adress of the instance.

   -  If the role for which the alarm is generated is HMaster, go to :ref:`2 <alm-19007__li56776013194753>`.
   -  If the role for which the alarm is generated is RegionServer, go to :ref:`3 <alm-19007__li29806005194753>`.

#. .. _alm-19007__li56776013194753:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the HMaster for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **GC** > **Garbage Collection (GC) Time of HMaster** and click **OK** to check whether the value of **GC time** **for old generation** is greater than the threshold (exceeds 5 seconds for three consecutive checks periods by default).

   -  If yes, go to :ref:`4 <alm-19007__li25514146194753>`.
   -  If no, go to :ref:`6 <alm-19007__li55997378194753>`.

#. .. _alm-19007__li29806005194753:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance** and click the RegionServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **GC** > **Garbage Collection (GC) Time of RegionServer** and click **OK** to check whether the value of **GC time** **for old generation** is greater than the threshold (exceeds 5 seconds for three consecutive checks periods by default).

   -  If yes, go to :ref:`4 <alm-19007__li25514146194753>`.
   -  If no, go to :ref:`6 <alm-19007__li55997378194753>`.

**Check the current JVM configuration.**

4. .. _alm-19007__li25514146194753:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations**, and click **All** **Configurations**. In Search, enter **GC_OPTS** to check the **GC_OPTS** memory parameter of role HMaster(HBase->HMaster), RegionServer(HBase->RegionServer). Adjust the values of **-Xmx** and **-XX:CMSInitiatingOccupancyFraction** of the GC_OPTS parameter by referring to the Note.

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
         -  **XX:CMSInitiatingOccupancyFraction** to be less than and equal to **85**, and it is calculated as follows: 100 x (hfile.block.cache.size + hbase.regionserver.global.memstore.size)

5. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-19007__li55997378194753>`.

**Collect fault information.**

6. .. _alm-19007__li55997378194753:

   On the FusionInsight Manager interface of active and standby clusters, choose **O&M** > **Log** > **Download**.

7. In the **Service** drop-down list box, select **HBase** in the required cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927717.png
