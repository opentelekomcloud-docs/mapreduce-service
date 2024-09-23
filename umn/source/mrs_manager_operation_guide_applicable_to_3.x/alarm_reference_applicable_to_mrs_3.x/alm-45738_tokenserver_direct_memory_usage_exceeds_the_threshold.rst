:original_name: ALM-45738.html

.. _ALM-45738:

ALM-45738 TokenServer Direct Memory Usage Exceeds the Threshold
===============================================================

Alarm Description
-----------------

The system checks the direct memory usage of the TokenServer service every 60 seconds. This alarm is generated when the direct memory usage of the TokenServer instance exceeds the threshold (80% of the maximum memory) for five consecutive times.

This alarm is automatically cleared when the system detects that the TokenServer direct memory usage is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45738    Major          Yes
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

Direct memory overflow may cause service unavailability.

Possible Causes
---------------

The direct memory of the TokenServer process is overused or the direct memory is inappropriately allocated.

Handling Procedure
------------------

**Check the direct memory usage.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms** > **ALM-45738 TokenServer Direct Memory Usage Exceeds the Threshold**. Check the location information of the alarm and view the host name of the instance for which the alarm is generated.

#. .. _alm-45738__li7677390:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Guardian**. On the page that is displayed, click the **Instance** tab. On this tab page, select the role corresponding to the host name of the instance for which the alarm is generated. Click the drop-down list in the upper right corner of the chart area and choose **Customize** > **CPU and Memory** > **TokenServer Direct Memory Usage**. Then click **OK**.

#. Check whether the direct memory used by TokenServer reaches the threshold (80% of the maximum direct memory by default).

   -  If yes, go to :ref:`4 <alm-45738__li10450762161055>`.
   -  If no, go to :ref:`6 <alm-45738__d0e43963>`.

#. .. _alm-45738__li10450762161055:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Guardian**. On the page that is displayed, click the **Instance** tab. On this tab page, choose **TokenServer** > **Instance Configuration**. Click **All Configurations**, and choose **TokenServer** > **System**. Set **-XX:MaxDirectMemorySize** in the **GC_OPTS** parameter to a larger value based on site requirements and save the configuration.

   .. note::

      If this alarm is generated, the direct memory configured for TokenServer cannot meet the direct memory required by the TokenServer process. You are advised to check the direct memory usage of TokenServer and change the value of **-XX:MaxDirectMemorySize** in **GC_OPTS** to the twice of the direct memory used by TokenServer. You can change the value based on the actual service scenario. Refer to :ref:`2 <alm-45738__li7677390>` to view the TokenServer direct memory usage.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45738__d0e43963>`.

   .. important::

      During service or instance restart, Guardian may fail to be accessed and jobs cannot access OBS.

**Collect fault information.**

6. .. _alm-45738__d0e43963:

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

.. |image1| image:: /_static/images/en-us_image_0000002008102489.png
