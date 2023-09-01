:original_name: ALM-16007.html

.. _ALM-16007:

ALM-16007 Hive GC Time Exceeds the Threshold
============================================

Description
-----------

The system checks the garbage collection (GC) time of the Hive service every 60 seconds. This alarm is generated when the detected GC time exceeds the threshold (exceeds 12 seconds for three consecutive checks.) To change the threshold, choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **Hive**. This alarm is cleared when the Hive GC time is shorter than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16007    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated.                                                                 |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role name for which the alarm is generated.                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the object (host ID) for which the alarm is generated.                                                             |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the GC time exceeds the threshold, Hive data read and write are affected.

Possible Causes
---------------

The memory of Hive instances is overused, the heap memory is inappropriately allocated. As a result, GCs occur frequently.

Procedure
---------

**Check the GC time.**

#. On the FusionInsight Manager portal, click **O&M > Alarm > Alarms** and select the alarm whose **Alarm ID** is **16007**. Then check the role name in **Location** and confirm the IP adress of the instance.

   -  If the role for which the alarm is generated is HiveServer, go to :ref:`2 <alm-16007__li6180447514380>`.
   -  If the role for which the alarm is generated is MetaStore, go to :ref:`3 <alm-16007__li3832089314380>`.

#. .. _alm-16007__li6180447514380:

   On the FusionInsight Manager portal, choose **Cluster** >\ *Name of the desired cluster* > **Services** > **Hive** > **Instance** and click the HiveServer for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **GC**, and select **Garbage Collection (GC) Time of HiveServer** and click **OK** to check whether the GC time is longer than 12 seconds.

   -  If yes, go to :ref:`4 <alm-16007__li542936514380>`.
   -  If no, go to :ref:`7 <alm-16007__li2731494414380>`.

#. .. _alm-16007__li3832089314380:

   On the FusionInsight Manager portal, choose **Cluster** >\ *Name of the desired* *cluster* > **Services** > **Hive** > **Instance** and click the MetaStore for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the **Chart** area and choose **Customize** > **GC**, and select **Garbage Collection (GC) Time of MetaStore** and click **OK** to check whether the GC time is longer than 12 seconds.

   -  If yes, go to :ref:`4 <alm-16007__li542936514380>`.
   -  If no, go to :ref:`7 <alm-16007__li2731494414380>`.

**Check the current JVM configuration.**

4. .. _alm-16007__li542936514380:

   On the FusionInsight Manager portal, choose **Cluster** >\ *Name of the desired cluster* > **Services > Hive > Configurations > All Configurations**. Choose **HiveServer/MetaStore** > **JVM**. Adjust the value of **-Xmx** in **HIVE_GC_OPTS/METASTORE_GC_OPTS** as the following rules. Click **Save**.

   .. note::

      Suggestions for GC parameter settings for the HiveServer:

      -  When the Hive GC time exceeds the threshold, change the value of **-Xmx** to twice the default value. For example, if **-Xmx** is set to 2 GB by default, change the value of **-Xmx** to 4 GB.

      -  You are advised to change the value of **-Xms** to set the ratio of **-Xms** and **-Xmx** to 1:2 to avoid performance problems when JVM dynamically.

      Suggestions for GC parameter settings for the MetaServer:

      -  When the Meta GC time exceeds the threshold, change the value of **-Xmx** to twice the default value. For example, if **-Xmx** is set to 2 GB by default, change the value of **-Xmx** to 4 GB.

      -  You are advised to change the value of **-Xms** to set the ratio of **-Xms** and **-Xmx** to 1:2 to avoid performance problems when JVM dynamically.

5. Click **More > Restart Service** to restart the service.

6. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-16007__li2731494414380>`.

**Collect fault information.**

7.  .. _alm-16007__li2731494414380:

    On the FusionInsight Manager portal of active and standby clusters, choose **O&M** > **Log > Download**.

8.  In the **Service**, select **Hive** in the required cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127545.png
