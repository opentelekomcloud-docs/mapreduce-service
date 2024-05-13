:original_name: ALM-17004.html

.. _ALM-17004:

ALM-17004 Oozie Heap Memory Usage Exceeds the Threshold
=======================================================

Description
-----------

The system checks the heap memory usage of the Oozie service every 60 seconds. The alarm is generated when the heap memory usage of a Metadata instance exceeds the threshold (95% of the maximum memory). The alarm is cleared when the heap memory usage is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
17004    Major          Yes
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

The heap memory overflow may cause a service breakdown.

Possible Causes
---------------

The heap memory of the Oozie instance is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check heap memory usage.**

#. On the MRS Manager portal, choose **O&M > Alarm** **> Alarms** > **Oozie Heap Memory Usage Exceeds the Threshold** > **Location**. Check the IP address of the instance involved in this alarm.

#. On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services** > **Oozie** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down menu in the chart area and choose **Customize** > **Memory** > **Oozie Heap Memory Resource Percentage**. Click **OK**.

#. Check whether the used heap memory of Oozie reaches the threshold (the default value is 95% of the maximum heap memory) specified for Oozie.

   -  If yes, go to :ref:`4 <alm-17004__en-us_topic_0070543677_d0e31653>`.
   -  If no, go to :ref:`6 <alm-17004__en-us_topic_0070543677_d0e31704>`.

#. .. _alm-17004__en-us_topic_0070543677_d0e31653:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services** > **Oozie** > **Configurations > All Configuration\ s**. Set Search **GC_OPTS** in the search box. Increase the value of **-Xmx** as required, and click **Save** > **OK**.

   .. note::

      Suggestions on GC parameter settings for Oozie:

      You are advised to set **-Xms** and **-Xmx** to the same value to prevent adverse impact on performance when JVM dynamically adjusts the heap memory size.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-17004__en-us_topic_0070543677_d0e31704>`.

**Collect fault information.**

6. .. _alm-17004__en-us_topic_0070543677_d0e31704:

   On the MRS Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **Oozie** in the required cluster from the **Service**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607918.png
