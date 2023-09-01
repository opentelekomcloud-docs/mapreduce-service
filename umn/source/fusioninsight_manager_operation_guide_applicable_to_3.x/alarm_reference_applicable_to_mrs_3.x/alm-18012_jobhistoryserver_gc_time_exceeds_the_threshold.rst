:original_name: ALM-18012.html

.. _ALM-18012:

ALM-18012 JobHistoryServer GC Time Exceeds the Threshold
========================================================

Description
-----------

The system checks the garbage collection (GC) duration of the JobHistoryServer process every 60 seconds. This alarm is generated when the GC duration exceeds the threshold (12 seconds by default).

This alarm is cleared when the GC duration is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18012    Major          Yes
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

A long GC duration of the JobHistoryServer process may interrupt the services.

Possible Causes
---------------

The heap memory of the JobHistoryServer instance is overused or the heap memory is inappropriately allocated. As a result, GCs occur frequently.

Procedure
---------

**Check the GC duration.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** > **ALM-18012 JobHistoryServer GC Time Exceeds the Threshold** > **Location** to check the IP address of the instance for which the alarm is generated.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **MapReduce** > **Instance** > **JobHistoryServer (IP address for which the alarm is generated)**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **Garbage Collection (GC) Time of the JobHistoryServer** to check the GC duration statistics of the Broker process collected every minute.

#. Check whether the GC duration of the JobHistoryServer process collected every minute exceeds the threshold (12 seconds by default).

   -  If yes, go to :ref:`4 <alm-18012__li29276260185822>`.
   -  If no, go to :ref:`7 <alm-18012__li36309760185822>`.

#. .. _alm-18012__li29276260185822:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **MapReduce** > **Configurations** > **All** **Configurations** > **JobHistoryServer** > **System** to increase the value of **GC_OPTS** parameter as required.

   .. note::

      The mapping between the number of historical tasks (10000) and the memory of the JobHistoryServer is as follows:

      -Xms30G -Xmx30G -XX:NewSize=1G -XX:MaxNewSize=2G

#. Save the configuration and restart the JobHistoryServer instance.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18012__li36309760185822>`.

**Collect fault information.**

7.  .. _alm-18012__li36309760185822:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select **JobHistoryServer** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448166.png
