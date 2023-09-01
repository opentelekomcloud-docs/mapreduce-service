:original_name: ALM-14017.html

.. _ALM-14017:

ALM-14017 NameNode Direct Memory Usage Exceeds the Threshold
============================================================

Description
-----------

The system checks the direct memory usage of the HDFS service every 30 seconds. This alarm is generated when the direct memory usage of a NameNode instance exceeds the threshold (90% of the maximum memory).

The alarm is cleared when the direct memory usage is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14017    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the available direct memory of the HDFS service is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the NameNode instance is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check the direct memory usage.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms.** On the displayed interface, click the drop-down button of **ALM-14017 NameNode Direct Memory Usage Exceeds the Threshold**. Then check the role name in **Location** and confirm the IP adress of the instance.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance** > **NameNode (IP address for which the alarm is generated)**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **Resource**, and select **NameNode Memory** to check the direct memory usage.

#. Check whether the used direct memory of NameNode reaches 90% of the maximum direct memory specified for NameNode by default.

   -  If yes, go to :ref:`4 <alm-14017__li5299688794211>`.
   -  If no, go to :ref:`8 <alm-14017__li1686819594211>`.

#. .. _alm-14017__li5299688794211:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations** > **NameNode** > **System** to check whether "-XX:MaxDirectMemorySize" exists in the **GC_OPTS** parameter.

   -  If yes, go to :ref:`5 <alm-14017__li817315147319>`.
   -  If no, go to :ref:`6 <alm-14017__li16393123713315>`.

#. .. _alm-14017__li817315147319:

   In the **GC_OPTS** parameter, delete "-XX:MaxDirectMemorySize". Save the configuration and restart the NameNode instance.

#. .. _alm-14017__li16393123713315:

   Check whether the **ALM-14007 NameNode Heap Memory Usage Exceeds the Threshold** exists.

   -  If yes, handle the alarm by referring to **ALM-14007 NameNode Heap Memory Usage Exceeds the Threshold**.
   -  If no, go to :ref:`7 <alm-14017__li812407194211>`.

#. .. _alm-14017__li812407194211:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14017__li1686819594211>`.

**Collect fault information.**

8.  .. _alm-14017__li1686819594211:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

9.  Select **NameNode** in the required cluster from the **Service**.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927522.png
