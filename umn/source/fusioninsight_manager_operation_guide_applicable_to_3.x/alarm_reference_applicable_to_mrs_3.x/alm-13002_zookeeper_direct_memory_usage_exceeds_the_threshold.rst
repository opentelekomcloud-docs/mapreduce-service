:original_name: ALM-13002.html

.. _ALM-13002:

ALM-13002 ZooKeeper Direct Memory Usage Exceeds the Threshold
=============================================================

Description
-----------

The system checks the direct memory usage of the ZooKeeper service every 30 seconds. The alarm is generated when the direct memory usage of a ZooKeeper instance exceeds the threshold (80% of the maximum memory).

When the **Trigger Count** is 1, this alarm is cleared when the ZooKeeper Direct memory usage is less than the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the ZooKeeper Direct memory usage is less than 80% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13002    Major          Yes
======== ============== ==========

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

If the available direct memory of the ZooKeeper service is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the ZooKeeper instance is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check the direct memory usage.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms**. On the displayed interface, click the drop-down button of **ZooKeeper Direct Memory Usage Exceeds the Threshold**. Check the IP address of the instance that reports the alarm.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Instance** > **quorumpeer(the IP address checked)**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **CPU and Memory**, and select **ZooKeeper Heap And Direct Buffer Resource Percentage**, click **OK**.

#. Check whether the used direct buffer memory of ZooKeeper reaches 80% of the maximum direct buffer memory specified for ZooKeeper.

   -  If yes, go to :ref:`4 <alm-13002__li57922773161213>`.
   -  If no, go to :ref:`8 <alm-13002__li43327670161213>`.

#. .. _alm-13002__li57922773161213:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Configurations** > **All** **Configurations** > **quorumpeer** > **System** to check whether "-XX:MaxDirectMemorySize" exists in the **GC_OPTS** parameter.

   -  If yes, in the **GC_OPTS** parameter, delete "-XX:MaxDirectMemorySize" and go to :ref:`5 <alm-13002__li51542910161213>`.
   -  If no, go to :ref:`6 <alm-13002__li16393123713315>`.

#. .. _alm-13002__li51542910161213:

   Save the configuration and restart the ZooKeeper service.

#. .. _alm-13002__li16393123713315:

   Check whether the **ALM-13004 ZooKeeper Heap Memory Usage Exceeds the Threshold** exists.

   -  If yes, handle the alarm by referring to **ALM-13004 ZooKeeper Heap Memory Usage Exceeds the Threshold**.
   -  If no, go to :ref:`7 <alm-13002__li56397739161213>`.

#. .. _alm-13002__li56397739161213:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-13002__li43327670161213>`.

**Collect fault information.**

8.  .. _alm-13002__li43327670161213:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

9.  Select **ZooKeeper** in the required cluster from the **Service**.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807869.png
