:original_name: ALM-23007.html

.. _ALM-23007:

ALM-23007 Garbage Collection (GC) Time of the Loader Process Exceeds the Threshold
==================================================================================

Description
-----------

The system checks GC time of the Loader process every 60 seconds. The alarm is generated when GC time of the Loader process exceeds the threshold (default value: **12 seconds**) for 5 consecutive times. The alarm is cleared when GC time is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
23007    Major          Yes
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

Loader service response is slow.

Possible Causes
---------------

The heap memory of the Loader instance is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check GC time.**

#. On the MRS Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Garbage Collection (GC) Time of the Loader Process Exceeds the Threshold** > **Location**. Check the host name of the instance involved in this alarm.

#. On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down menu in the chart area and choose **Customize** > **GC** > **Garbage Collection (GC) Time of Loader**. Click **OK**.

#. Check whether GC time of the Loader process every second exceeds the threshold (default value: **12 seconds**).

   -  If yes, go to :ref:`4 <alm-23007__le43836763c17495db009983a29fba3de>`.
   -  If no, go to :ref:`6 <alm-23007__en-us_topic_0070543531_d0e42747>`.

#. .. _alm-23007__le43836763c17495db009983a29fba3de:

   On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader** > **Configurations**. Click **All Configurations**. Search **LOADER_GC_OPTS** in the search box. Increase the value of **-Xmx** as required, and click **Save**. Click **OK**.

   .. note::

      If this alarm is generated, the heap memory configured for the current Loader instance cannot meet the heap memory required for data transmission. You are advised to handle the problem by referring to :ref:`4 <alm-23004__en-us_topic_0070543528_d0e41794>` in section :ref:`ALM-23004 Loader Heap Memory Usage Exceeds the Threshold <alm-23004>`.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-23007__en-us_topic_0070543531_d0e42747>`.

**Collect fault information.**

6. .. _alm-23007__en-us_topic_0070543531_d0e42747:

   On the MRS Manager portal, choose **O&M** > **Log** > **Download**.

7. Select **Loader** in the required cluster from the **Service** drop-down list.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807565.png
