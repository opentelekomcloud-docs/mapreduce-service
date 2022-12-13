:original_name: ALM-38002.html

.. _ALM-38002:

ALM-38002 Kafka Heap Memory Usage Exceeds the Threshold
=======================================================

Description
-----------

The system checks the Kafka service status every 30 seconds. The alarm is generated when the heap memory usage of a Kafka instance exceeds the threshold (95% of the maximum memory) for 10 consecutive times.

When the **Trigger Count** is 1, this alarm is cleared when the heap memory usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the heap memory usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38002    Major          Yes
======== ============== =====================

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

If the available Kafka heap memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The heap memory of the Kafka instance is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check heap memory usage.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Kafka Heap Memory Usage Exceeds the Threshold** > **Location**. Check the host name of the instance involved in this alarm.

#. .. _alm-38002__li118928315563:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down list in the upper right corner of the chart area, choose **Customize** > **Process** > **Heap Memory Usage of Kafka**, and click **OK**.

#. Check whether the used heap memory of Kafka reaches 95% of the maximum heap memory specified for Kafka.

   -  If yes, go to :ref:`4 <alm-38002__li1593445465720>`.
   -  If no, go to :ref:`6 <alm-38002__li3623590715563>`.

**Check the heap memory size configured for Kafka.**

4. .. _alm-38002__li1593445465720:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations** > **All** **Configurations**> **Broker(Role)** > **Environment**. Increase the value of **KAFKA_HEAP_OPTS** by referring to the Note.

   .. note::

      -  It is recommended that **-Xmx** and **-Xms** be set to the same value.
      -  You are advised to view **Heap Memory Usage of Kafka** by referring to :ref:`2 <alm-38002__li118928315563>`, and set the value of **KAFKA_HEAP_OPTS** to twice the value of **Heap Memory Used by Kafka.**

5. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-38002__li3623590715563>`.

**Collect fault information.**

6. .. _alm-38002__li3623590715563:

   On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **Kafka** in the required cluster from the **Service** drop-down list.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417501.png
