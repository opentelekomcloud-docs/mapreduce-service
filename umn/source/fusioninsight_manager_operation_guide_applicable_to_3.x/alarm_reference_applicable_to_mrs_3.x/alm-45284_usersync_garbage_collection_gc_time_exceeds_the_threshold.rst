:original_name: ALM-45284.html

.. _ALM-45284:

ALM-45284 UserSync Garbage Collection (GC) Time Exceeds the Threshold
=====================================================================

Description
-----------

The system checks the GC duration of the UserSync process every 60 seconds. This alarm is generated when the GC duration of the UserSync process exceeds the threshold (12 seconds by default) for five consecutive times. This alarm is cleared when the GC duration is less than the threshold.

Attributes
----------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
45284    Major          Yes
======== ============== =====================

Parameters
----------

================= =========================================
Name              Meaning
================= =========================================
Source            Cluster for which the alarm is generated.
ServiceName       Service for which the alarm is generated.
RoleName          Role for which the alarm is generated.
HostName          Host for which the alarm is generated.
Trigger Condition Threshold for triggering the alarm.
================= =========================================

Impact on the System
--------------------

UserSync responds slowly.

Possible Causes
---------------

The heap memory of the UserSync instance is overused or the heap memory is inappropriately allocated. As a result, GCs occur frequently.

Procedure
---------

**Check the GC time.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45284 UserSync Garbage Collection (GC) Time Exceeds the Threshold**. Check the location information of the alarm and view the host name of the instance for which the alarm is generated.

#. .. _alm-45284__li43047473:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Ranger** > **Instance**. Select the role corresponding to the host name of the instance for which the alarm is generated and click the drop-down list in the upper right corner of the chart area. Choose **Customize** > **GC** > **UserSync GC Duration**. Click **OK**.

#. Check whether the GC duration of the UserSync process collected every minute exceeds the threshold (12 seconds by default).

   -  If yes, go to :ref:`4 <alm-45284__d0e44388>`.
   -  If no, go to :ref:`6 <alm-45284__d0e44409>`.

#. .. _alm-45284__d0e44388:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Ranger** > **Instance** > **UserSync** > **Instance Configuration**. Click **All Configurations**, and choose **UserSync** > **System**. Increase the value of **-Xmx** in the **GC_OPTS** parameter based on the site requirements and save the configuration.

   .. note::

      If this alarm is generated, the heap memory configured for UserSync cannot meet the heap memory required by the UserSync process. You are advised to change the value of **GC_OPTS** to the twice that of the heap memory used by UserSync. You can change the value based on the actual service scenario. For details about how to check the UserSync heap memory usage, see :ref:`2 <alm-45284__li43047473>`.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45284__d0e44409>`.

**Collect the fault information.**

6. .. _alm-45284__d0e44409:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Ranger** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault that triggers the alarm is rectified, the alarm is automatically cleared.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0293267262.png
