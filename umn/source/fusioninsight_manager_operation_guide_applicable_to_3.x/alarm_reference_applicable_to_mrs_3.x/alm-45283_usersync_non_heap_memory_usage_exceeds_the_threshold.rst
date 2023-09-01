:original_name: ALM-45283.html

.. _ALM-45283:

ALM-45283 UserSync Non Heap Memory Usage Exceeds the Threshold
==============================================================

Description
-----------

The system checks the non-heap memory usage of the UserSync service every 60 seconds. This alarm is generated when the non-heap memory usage of the UserSync instance exceeds the threshold (80% of the maximum memory) for five consecutive times. This alarm is cleared when the non-heap memory usage is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45283    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Non-heap memory overflow may cause service breakdown.

Possible Causes
---------------

The non-heap memory of the UserSync process is overused or the non-heap memory is inappropriately allocated.

Procedure
---------

**Check non-heap memory usage.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45283 UserSync Non Heap Memory Usage Exceeds the Threshold**. Check the location information of the alarm and view the host name of the instance for which the alarm is generated.

#. On FusionInsight Manager, choose **Cluster** > **Services** > **Ranger** > **Instance**. Select the role corresponding to the host name of the instance for which the alarm is generated. Click the drop-down list in the upper right corner of the chart area and choose **Customize** > **CPU and Memory** > **UserSync Non Heap Memory Usage**. Click **OK**.

#. Check whether the non-heap memory used by UserSync reaches the threshold (80% of the maximum non-heap memory by default).

   -  If yes, go to :ref:`4 <alm-45283__li29985659161559>`.
   -  If no, go to :ref:`6 <alm-45283__d0e44186>`.

#. .. _alm-45283__li29985659161559:

   On FusionInsight Manager, choose **Cluster** > **Services** > **Ranger** > **Instance** > **UserSync** > **Instance Configuration**. Click **All Configurations**, and choose **UserSync** > **System**. Set **-XX: MaxPermSize** in the **GC_OPTS** parameter to a larger value based on site requirements and click **Save** to save the configuration.

   .. note::

      If this alarm is generated, the non-heap memory size configured for the UserSync instance cannot meet the non-heap memory required by the UserSync process. You are advised to change the **-XX:MaxPermSize** value of **GC_OPTS** to twice that of the current non-heap memory size or change the value based on the site requirements.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45283__d0e44186>`.

**Collect the fault information.**

6. .. _alm-45283__d0e44186:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Ranger** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448146.png
