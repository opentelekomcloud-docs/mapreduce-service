:original_name: ALM-17007.html

.. _ALM-17007:

ALM-17007 Garbage Collection (GC) Time of the Oozie Process Exceeds the Threshold
=================================================================================

Description
-----------

The system checks GC time of the Oozie process every 60 seconds. The alarm is generated when GC time of the Oozie process exceeds the threshold (default value: **12 seconds**). The alarm is cleared when GC time is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
17007    Major          Yes
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

Oozie responds slowly when it is used to submit tasks.

Possible Causes
---------------

The heap memory of the Oozie instance is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check GC time.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Garbage Collection (GC) Time of the Oozie Process Exceeds the Threshold** > **Location**. Check the IP address of the instance involved in this alarm.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services** > **Oozie** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down menu in the chart area and choose **Customize** > **GC** > **Garbage Collection (GC) Time of Oozie**. Click **OK**.

#. Check whether GC time of the Oozie process every second exceeds the threshold (default value: **12 seconds**).

   -  If yes, go to :ref:`4 <alm-17007__l054b8501eb0f42fc8d5e96d6a497ec94>`.
   -  If no, go to :ref:`6 <alm-17007__en-us_topic_0070543680_d0e32615>`.

#. .. _alm-17007__l054b8501eb0f42fc8d5e96d6a497ec94:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services** > **Oozie** > **Configurations**. Click **All Configurations**. Search **GC_OPTS** in the search box. Increase the value of **-Xmx** as required, and click **Save**. Click **OK**.

   .. note::

      Suggestions on GC parameter settings for Oozie:

      You are advised to set **-Xms** and **-Xmx** to the same value to prevent adverse impact on performance when JVM dynamically adjusts the heap memory size.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-17007__en-us_topic_0070543680_d0e32615>`.

**Collect fault information.**

6. .. _alm-17007__en-us_topic_0070543680_d0e32615:

   On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **Oozie** in the required cluster from the **Service** drop-down list.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927857.png
