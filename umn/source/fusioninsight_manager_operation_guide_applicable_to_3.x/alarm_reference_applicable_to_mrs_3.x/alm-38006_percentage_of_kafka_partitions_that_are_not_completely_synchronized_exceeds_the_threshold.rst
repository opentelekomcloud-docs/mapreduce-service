:original_name: ALM-38006.html

.. _ALM-38006:

ALM-38006 Percentage of Kafka Partitions That Are Not Completely Synchronized Exceeds the Threshold
===================================================================================================

Description
-----------

The system checks the percentage of Kafka partitions that are not completely synchronized to the total number of partitions every 60 seconds. This alarm is generated when the percentage exceeds the threshold (50% by default) for 3 consecutive times.

When the **Trigger Count** is 1, this alarm is cleared when the percentage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the percentage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38006    Major          Yes
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
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Too many Kafka partitions that are not completely synchronized affect service reliability. In addition, data may be lost when leaders are switched.

Possible Causes
---------------

Some nodes where the Broker instance resides are abnormal or stop running. As a result, replicas of some partitions in Kafka are out of the in-sync replicas (ISR) set.

Procedure
---------

**Check Broker instances.**

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. The Kafka instances page is displayed.

#. .. _alm-38006__li1743646315478:

   Check whether faulty nodes exist among all Broker nodes.

   -  If yes, record the host name of the node and go to :ref:`3 <alm-38006__li2760667615478>`.
   -  If no, go to :ref:`5 <alm-38006__li6648467215478>`.

#. .. _alm-38006__li2760667615478:

   On the FusionInsight Manager portal, click **O&M** > **Alarm** > **Alarms** to check whether the fault described in :ref:`2 <alm-38006__li1743646315478>` exists in the alarm information and handle the alarm based on corresponding methods.

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. The Kafka instances page is displayed.

#. .. _alm-38006__li6648467215478:

   Check whether stopped nodes exist among all Broker instance.

   -  If yes, go to :ref:`6 <alm-38006__li1472641115478>`.
   -  If no, go to :ref:`7 <alm-38006__li5037705315478>`.

#. .. _alm-38006__li1472641115478:

   Select all stopped Broker instances and click **Start Instance**.

#. .. _alm-38006__li5037705315478:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-38006__li1632355415478>`.

**Collect fault information.**

8.  .. _alm-38006__li1632355415478:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

9.  Select **Kafka** in the required cluster from the **Service** drop-down list.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927557.png
