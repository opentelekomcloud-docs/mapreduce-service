:original_name: ALM-45740.html

.. _ALM-45740:

ALM-45740 TokenServer GC Duration Exceeds the Threshold
=======================================================

Alarm Description
-----------------

The system checks the GC duration of the TokenServer process every 60 seconds. This alarm is generated when the GC duration of the TokenServer process exceeds the threshold (12 seconds by default) for five consecutive times.

This alarm is automatically cleared when the system detects that the GC duration is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45740    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+----------------------------------------------------------+
| Parameter         | Description                                              |
+===================+==========================================================+
| Source            | Specifies the cluster for which the alarm was generated. |
+-------------------+----------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm was generated. |
+-------------------+----------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm was generated.    |
+-------------------+----------------------------------------------------------+
| HostName          | Specifies the host for which the alarm was generated.    |
+-------------------+----------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.        |
+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

TokenServer responds slowly.

Possible Causes
---------------

The heap memory of the TokenServer process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Handling Procedure
------------------

**Check the GC duration.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms** > **ALM-45740 TokenServer GC Duration Exceeds the Threshold**. Check the location information of the alarm and view the host name of the instance for which the alarm is generated.

#. .. _alm-45740__li43047473:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Guardian**. On the page that is displayed, click the **Instance** tab. On this tab page, select the role corresponding to the host name of the instance for which the alarm is generated and click the drop-down list in the upper right corner of the chart area. Choose **Customize** > **GC** > **TokenServer GC Duration**. Then click **OK**.

#. Check whether the GC duration of the TokenServer process collected every minute exceeds the threshold (12 seconds by default).

   -  If yes, go to :ref:`4 <alm-45740__d0e44388>`.
   -  If no, go to :ref:`6 <alm-45740__d0e44409>`.

#. .. _alm-45740__d0e44388:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Guardian**. On the page that is displayed, click the **Instance** tab. On this tab page, choose **TokenServer** > **Instance Configuration**. Click **All Configurations**, and choose **TokenServer** > **System**. Set **-Xmx** in the **GC_OPTS** parameter to a larger value based on site requirements and save the configuration.

   .. note::

      If this alarm is generated, the heap memory configured for TokenServer cannot meet the heap memory required by the TokenServer process. You are advised to change the value of **-Xmx** in **GC_OPTS** to twice that of the heap memory used by TokenServer. You can change the value based on the actual service scenario. Refer to :ref:`2 <alm-45740__li43047473>` to view the TokenServer heap memory usage.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45740__d0e44409>`.

   .. important::

      During service or instance restart, Guardian may fail to be accessed and jobs cannot access OBS.

**Collect fault information.**

6. .. _alm-45740__d0e44409:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Guardian** for the destination cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002008102517.png
