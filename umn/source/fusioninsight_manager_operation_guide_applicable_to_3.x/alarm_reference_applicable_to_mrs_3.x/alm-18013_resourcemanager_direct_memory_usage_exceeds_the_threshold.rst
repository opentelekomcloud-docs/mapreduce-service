:original_name: ALM-18013.html

.. _ALM-18013:

ALM-18013 ResourceManager Direct Memory Usage Exceeds the Threshold
===================================================================

Description
-----------

The system checks the direct memory usage of the Yarn service every 30 seconds. This alarm is generated when the direct memory usage of a ResourceManager instance exceeds the threshold (90% of the maximum memory).

The alarm is cleared when the direct memory usage is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18013    Major          Yes
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

If the available direct memory of the Yarn service is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the ResourceManager instance is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check the direct memory usage.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** > **ALM-18013 ResourceManager Direct Memory Usage Exceeds the Threshold** > **Location** to check the IP address of the instance for which the alarm is generated.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Yarn** > **Instance** > **ResourceManager (IP address for which the alarm is generated)**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **Memory Usage Status of ResourceManager** to check the direct memory usage.

#. Check whether the used direct memory of ResourceManager reaches 90% of the maximum direct memory specified for ResourceManager by default.

   -  If yes, go to :ref:`4 <alm-18013__li3060052619112>`.
   -  If no, go to :ref:`9 <alm-18013__li1521968019112>`.

#. .. _alm-18013__li3060052619112:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Yarn** > **Configurations** > **All** **Configurations** > **ResourceManager** > **System** to increase the value of check whether **-XX:MaxDirectMemorySize** exists in the **GC_OPTS** parameter.

   -  If yes, go to :ref:`5 <alm-18013__li28439618491>`.
   -  If no, go to :ref:`7 <alm-18013__li558791074715>`.

#. .. _alm-18013__li28439618491:

   In the **GC_OPTS** parameter, delete **-XX:MaxDirectMemorySize**.

#. Save the configuration and restart the ResourceManager instance.

#. .. _alm-18013__li558791074715:

   Check whether the **ALM-18008 Heap Memory Usage of ResourceManager Exceeds the Threshold** exists.

   -  If yes, handle the alarm by referring to **ALM-18008 Heap Memory Usage of ResourceManager Exceeds the Threshold**.
   -  If no, go to :ref:`8 <alm-18013__li2441573219112>`.

#. .. _alm-18013__li2441573219112:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-18013__li1521968019112>`.

**Collect fault information.**

9.  .. _alm-18013__li1521968019112:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

10. Select **ResourceManager** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807685.png
