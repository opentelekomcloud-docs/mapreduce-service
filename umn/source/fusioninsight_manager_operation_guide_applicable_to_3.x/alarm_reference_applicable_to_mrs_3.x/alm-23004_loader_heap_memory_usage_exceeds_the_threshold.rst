:original_name: ALM-23004.html

.. _ALM-23004:

ALM-23004 Loader Heap Memory Usage Exceeds the Threshold
========================================================

Description
-----------

The system checks the heap memory usage of the Loader service every 60 seconds. The alarm is generated when the heap memory usage of a Loader instance exceeds the threshold (95% of the maximum memory) for 10 consecutive times. The alarm is cleared when the heap memory usage is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
23004    Major          Yes
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

The heap memory of the Loader instance is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check heap memory usage.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Loader Heap Memory Usage Exceeds the Threshold** > **Location.** Check the host name of the instance involved in this alarm.

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down menu in the chart area and choose **Customize** > **Memory** > **Loader Heap Memory Resource Percentage**. Click **OK**.

#. Check whether the used heap memory of Loader reaches the threshold (the default value is 95% of the maximum heap memory) specified for Loader.

   -  If yes, go to :ref:`4 <alm-23004__en-us_topic_0070543528_d0e41794>`.
   -  If no, go to :ref:`6 <alm-23004__en-us_topic_0070543528_d0e41845>`.

#. .. _alm-23004__en-us_topic_0070543528_d0e41794:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader** > **Configurations**. Click **All Configurations**. Increase the value of **-Xmx** in **GC_OPTS** as required, and click **Save**. Click **OK**.

   .. note::

      -  If this alarm is generated, the heap memory configured for the current Loader instance is insufficient for data transmission. You are advised to open the instance monitoring page, display the Loader heap memory resource status monitoring chart, and observe the change trend of the heap memory used by Loader in the monitoring chart. Then change the value of **-Xmx** to twice the current heap memory usage or to another value to meet site requirements.
      -  When setting the heap memory, you can set **-Xms** and **-Xmx** to similar values to avoid performance deterioration caused by heap size adjustment after each GC.
      -  Ensure that the sum of **-Xmx** and **XX:MaxPermSize** is not greater than the physical memory of the node server.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-23004__en-us_topic_0070543528_d0e41845>`.

**Collect fault information.**

6. .. _alm-23004__en-us_topic_0070543528_d0e41845:

   On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **Loader** in the required cluster from the **Service** drop-down list.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927550.png
