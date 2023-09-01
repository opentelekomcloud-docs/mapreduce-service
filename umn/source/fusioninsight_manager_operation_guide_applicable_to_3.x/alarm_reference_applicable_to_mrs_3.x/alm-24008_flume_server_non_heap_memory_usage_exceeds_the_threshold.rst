:original_name: ALM-24008.html

.. _ALM-24008:

ALM-24008 Flume Server Non Heap Memory Usage Exceeds the Threshold
==================================================================

Description
-----------

The system checks the non-heap memory usage of the Flume service every 60 seconds. This alarm is generated when the non-heap memory usage of the Flume instance exceeds the threshold (80% of the maximum memory) for five consecutive times. This alarm is cleared when the non-heap memory usage is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24008    Major          Yes
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

The non-heap memory of the Flume instance is overused or the non-heap memory is inappropriately allocated.

Procedure
---------

**Check non-heap memory usage.**

#. Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing **Flume Non Heap Memory Usage Exceeds the Threshold**, and view the **Location** information. Check the name of the host for which the alarm is generated.

#. On FusionInsight Manager, choose **Cluster** > *Name of the target cluster* > **Services** > **Flume**. On the page that is displayed, click the **Instance** tab. On the displayed tab page, select the role corresponding to the host name for which the alarm is generated and select **Customize** from the drop-down list in the upper right corner of the chart area. Choose **Agent** and select **Flume Non Heap Memory Resource Percentage**. Then, click **OK**.

#. Check whether the non-heap memory used by Flume reaches the threshold (80% of the maximum non-heap memory by default).

   -  If yes, go to :ref:`4 <alm-24008__li29985659161559>`.
   -  If no, go to :ref:`6 <alm-24008__d0e44186>`.

#. .. _alm-24008__li29985659161559:

   On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **Flume** > **Configuration**. On the page that is displayed, click **All Configurations** and choose **Flume** > **System**. Set **-XX: MaxPermSize** in the **GC_OPTS** parameter to a larger value based on site requirements and save the configuration.

   .. note::

      If this alarm is generated, the non-heap memory size configured for the Flume server instance cannot meet service requirements. You are advised to change the value of **-XX:MaxPermSize** to twice the current non-heap memory size or change the value based on site requirements.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-24008__d0e44186>`.

**Collect the fault information.**

6. .. _alm-24008__d0e44186:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767398.png
