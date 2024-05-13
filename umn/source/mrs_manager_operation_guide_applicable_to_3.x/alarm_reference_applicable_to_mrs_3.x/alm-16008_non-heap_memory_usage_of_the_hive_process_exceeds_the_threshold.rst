:original_name: ALM-16008.html

.. _ALM-16008:

ALM-16008 Non-Heap Memory Usage of the Hive Process Exceeds the Threshold
=========================================================================

Description
-----------

The system checks the Hive service status every 30 seconds. The alarm is generated when the non-heap memory usage of an Hive service exceeds the threshold (95% of the maximum memory).

Users can choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **Hive** to change the threshold.

The alarm is cleared when the non-heap memory usage is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16008    Major          Yes
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

When the non-heap memory usage of Hive is overhigh, the performance of Hive task operation is affected. In addition, a memory overflow may occur so that the Hive service is unavailable.

Possible Causes
---------------

The non-heap memory of the Hive instance on the node is overused or the non-heap memory is inappropriately allocated. As a result, the usage exceeds the threshold.

Procedure
---------

**Check non-heap memory usage.**

#. On the MRS Manager portal, click **O&M > Alarm > Alarms** and select the alarm whose **Alarm ID** is **16008**. Then check the role name in **Location** and confirm the IP adress of the instance.

   -  If the role for which the alarm is generated is HiveServer, go to :ref:`2 <alm-16008__li54453327144225>`.
   -  If the role for which the alarm is generated is MetaStore, go to :ref:`3 <alm-16008__li31617556144225>`.

#. .. _alm-16008__li54453327144225:

   On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Instance** and click the HiveServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory**, and select **HiveServer Memory Usage Statistics** and click **OK**, check whether the used non-heap memory of the HiveServer service reaches the threshold(default value: 95%) of the maximum non-heap memory specified for HiveServer.

   -  If yes, go to :ref:`4 <alm-16008__li24754013144225>`.
   -  If no, go to :ref:`7 <alm-16008__li3071924144225>`.

#. .. _alm-16008__li31617556144225:

   On the MRS Manager portal, choose **Cluster** > *Name of the desired* *cluster* > **Services** > **Hive** > **Instance** and click the MetaStore for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory**, and select **MetaStore Memory Usage Statistics** and click **OK**, check whether the used non-heap memory of the MetaStore service reaches the threshold(default value: 95%) of the maximum non-heap memory specified for MetaStore.

   -  If yes, go to :ref:`4 <alm-16008__li24754013144225>`.
   -  If no, go to :ref:`7 <alm-16008__li3071924144225>`.

#. .. _alm-16008__li24754013144225:

   On the MRS Manager portal, choose **Cluster** **>** *Name of the desired* *cluster* > **Services** > **Hive** > **Configurations > All Configurations**. Choose **HiveServer/MetaStore** > **JVM**. Adjust the value of **-XX:MaxMetaspaceSize** in **HIVE_GC_OPTS/METASTORE_GC_OPTS** as the following rules. Click **Save**.

   .. note::

      Suggestions for GC parameter settings for the HiveServer:

      -  It is recommended that you set the value of **-XX:MaxMetaspaceSize** to 1/8 of the value of **-Xmx**. For example, if **-Xmx** is set to 2 GB, **-XX:**

         **MaxMetaspaceSize** is set to 256 MB. If **-Xmx** is set to 4 GB, **-XX:MaxMetaspaceSize** is set to 512 MB.

      Suggestions for GC parameter settings for the MetaServer:

      -  It is recommended that you set the value of **-XX:MaxMetaspaceSize** to 1/8 of the value of **-Xmx**. For example, if **-Xmx** is set to 2 GB, **-XX:**

         **MaxMetaspaceSize** is set to 256 MB. If **-Xmx** is set to 4 GB, **-XX:MaxMetaspaceSize** is set to 512 MB

#. Click **More > Restart Service** to restart the service.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-16008__li3071924144225>`.

**Collect fault information.**

7.  .. _alm-16008__li3071924144225:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

8.  Select **Hive** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087385.png
