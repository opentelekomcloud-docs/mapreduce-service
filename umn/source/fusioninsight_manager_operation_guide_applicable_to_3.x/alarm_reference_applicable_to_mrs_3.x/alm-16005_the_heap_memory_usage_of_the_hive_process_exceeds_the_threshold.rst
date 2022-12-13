:original_name: ALM-16005.html

.. _ALM-16005:

ALM-16005 The Heap Memory Usage of the Hive Process Exceeds the Threshold
=========================================================================

Description
-----------

The system checks the Hive service status every 30 seconds. The alarm is generated when the heap memory usage of an Hive service exceeds the threshold (95% of the maximum memory).

Users can choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **Hive** to change the threshold.

The alarm is cleared when the heap memory usage is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16005    Major          Yes
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

When the heap memory usage of Hive is overhigh, the performance of Hive task operation is affected. In addition, a memory overflow may occur so that the Hive service is unavailable.

Possible Causes
---------------

The heap memory of the Hive instance on the node is overused or the heap memory is inappropriately allocated. As a result, the usage exceeds the threshold.

Procedure
---------

**Check heap memory usage.**

#. On the FusionInsight Manager portal, click **O&M > Alarm > Alarms** and select the alarm whose **Alarm ID** is **16005**. Then check the role name in **Location** and confirm the IP adress of the instance.

   -  If the role for which the alarm is generated is HiveServer, go to :ref:`2 <alm-16005__li2900058143018>`.
   -  If the role for which the alarm is generated is MetaStore, go to :ref:`3 <alm-16005__li46068501143018>`.

#. .. _alm-16005__li2900058143018:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* **> Services** > **Hive** > **Instance** and click the HiveServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory**, and select **HiveServer Memory Usage Statistics** and click **OK**, check whether the used heap memory of the HiveServer service reaches the threshold(default value: 95%) of the maximum heap memory specified for HiveServer.

   -  If yes, go to :ref:`4 <alm-16005__li39802450143018>`.
   -  If no, go to :ref:`7 <alm-16005__li7710755143018>`.

#. .. _alm-16005__li46068501143018:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Instance** and click the MetaStore for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **CPU and Memory**, and select **MetaStore Memory Usage Statistics** and click **OK**, check whether the used heap memory of the MetaStore service reaches the threshold(default value: 95%) of the maximum heap memory specified for MetaStore.

   -  If yes, go to :ref:`4 <alm-16005__li39802450143018>`.
   -  If no, go to :ref:`7 <alm-16005__li7710755143018>`.

#. .. _alm-16005__li39802450143018:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations > All Configurations**. Choose **HiveServer/MetaStore** > **JVM**. Adjust the value of **-Xmx** in **HIVE_GC_OPTS/METASTORE_GC_OPTS** as the following rules. Click **Save**.

   .. note::

      Suggestions for GC parameter settings for the HiveServer:

      -  When the heap memory used by the HiveServer process reaches the threshold (default value: 95%) of the maximum heap memory set by the HiveServer process, change the value of **-Xmx** to twice the default value. For example, if **-Xmx** is set to 2GB by default, change the value of **-Xmx** to 4GB. You are advised to change the value of **-Xms** to set the ratio of **-Xms** and **-Xmx** to 1:2 to avoid performance problems when JVM dynamically. On the FusionInsight Manager home page, choose **O&M**> **Alarm**> **Thresholds** > *Name of the desired cluster* **> Hive** > **CPU and Memory** > **HiveServer Heap Memory Usage Statistics (HiveServer)** to view **Threshold**.

      Suggestions for GC parameter settings for the MetaServer:

      -  When the heap memory used by the MetaStore process reaches the threshold (default value: 95%) of the maximum heap memory set by the MetaStore process, change the value of **-Xmx** to twice the default value. For example, if **-Xmx** is set to 2GB by default, change the value of **-Xmx** to 4GB. On the FusionInsight Manager home page, choose **O&M**> **Alarm**> **Thresholds** > *Name of the desired cluster* **> Hive** > **CPU and Memory** > **MetaStore Heap Memory Usage Statistics (MetaStore)** to view **Threshold**.

      -  You are advised to change the value of **-Xms** to set the ratio of **-Xms** and **-Xmx** to 1:2 to avoid performance problems when JVM dynamically.

#. Click **More > Restart Service** to restart the service.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-16005__li7710755143018>`.

**Collect fault information.**

7.  .. _alm-16005__li7710755143018:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select **Hive** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417381.png
