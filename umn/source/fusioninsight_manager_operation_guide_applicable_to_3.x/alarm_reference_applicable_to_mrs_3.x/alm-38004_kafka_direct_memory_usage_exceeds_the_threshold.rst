:original_name: ALM-38004.html

.. _ALM-38004:

ALM-38004 Kafka Direct Memory Usage Exceeds the Threshold
=========================================================

Description
-----------

The system checks the direct memory usage of the Kafka service every 30 seconds. This alarm is generated when the direct memory usage of a Kafka instance exceeds the threshold (80% of the maximum memory) for 10 consecutive times.

When the **Trigger Count** is 1, this alarm is cleared when the direct memory usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the direct memory usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38004    Major          Yes
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

If the available direct memory of the Kafka service is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the Kafka instance is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check the direct memory usage.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Kafka Direct Memory Usage Exceeds the Threshold** > **Location** to check the host name of the instance for which the alarm is generated.

#. .. _alm-38004__li28837961155343:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down menu in the Chart area and choose **Customize** > **Process** > **Kafka** **Direct Memory Usage**, and click **OK**.

#. Check whether the used direct memory of Kafka reaches 80% of the maximum direct memory specified for Kafka.

   -  If yes, go to :ref:`4 <alm-38004__li11113491818>`.
   -  If no, go to :ref:`7 <alm-38004__li52892950155343>`.

**Check the direct memory size configured for the Kafka.**

4. .. _alm-38004__li11113491818:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations** > **All** **Configurations** > **Broker(Role)** > **Environment** to increase the value of **-Xmx** configured in the **KAFKA_HEAP_OPTS** parameter by referring to the Note.

   .. note::

      -  It is recommended that **-Xmx** and **-Xms** be set to the same value.
      -  You are advised to view **Kafka** **Direct Memory Usage** by referring to :ref:`2 <alm-38004__li28837961155343>`, and set the value of **KAFKA_HEAP_OPTS** to twice the value of **Direct Memory Used by Kafka.**

5. Save the configuration and restart the Kafka service.

6. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-38004__li52892950155343>`.

**Collect fault information.**

7.  .. _alm-38004__li52892950155343:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

8.  Select **Kafka** in the required cluster from the **Service** drop-down list.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417502.png
