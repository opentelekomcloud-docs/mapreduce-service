:original_name: ALM-45010.html

.. _ALM-45010:

ALM-45010 HSBroker GC Duration Exceeds the Threshold
====================================================

Alarm Description
-----------------

The system checks the garbage collection (GC) duration of the HSBroker process every 60 seconds. This alarm is generated when the GC duration of the HSBroker process exceeds the threshold (12,000 ms by default) for three consecutive times.

This alarm is automatically cleared when the system detects that the GC duration is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45010    Major          No
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

HSBroker may respond slowly, the HSConsole page cannot be refreshed, and the access to HSBroker may be interrupted.

Possible Causes
---------------

The heap memory of the HSBroker process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Handling Procedure
------------------

**Check the GC duration of the HSBroker process.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45010 HSBroker GC Duration Exceeds the Threshold**. In the **Location** field of the alarm details, check the instance host name for which the alarm is generated.

#. .. _alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_li43047473:

   Choose **Cluster** > **Services** > **HetuEngine** > **Instances** and click the instance host name for which the alarm is generated. Click the drop-down list in the upper right corner of the chart area, choose **Customize** > **GC** > **GC Duration of the HSBroker Process**, and click **OK**.

#. Check whether the GC duration of the HSBroker process collected every minute exceeds the threshold (12,000 ms by default).

   -  If yes, go to :ref:`4 <alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_d0e44388>`.
   -  If no, go to :ref:`6 <alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_d0e44409>`.

#. .. _alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_d0e44388:

   Choose **Cluster** > **Services** > **HetuEngine** > **Instances** > **HSBroker** > **Instance Configurations** > **All Configurations**, and select **HSBroker** > **Tuning**. Set **-Xmx** in the **GC_OPTS** parameter to a larger value based on site requirements and save the configuration.

   .. note::

      If this alarm is generated, the heap memory configured for HSBroker cannot meet the heap memory required by the HSBroker process. You are advised to change the value of **-Xmx** in **GC_OPTS** to the twice that of the heap memory used by HSBroker. You can change the value based on the actual service scenario. For details about how to check the HSBroker heap memory usage, see :ref:`2 <alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_li43047473>`.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_d0e44409>`.

   .. caution::

      During the restart of the service or instance, HSBroker may fail to be accessed.

**Collect fault information.**

6. .. _alm-45010__en-us_topic_0000002555105909_en-us_topic_0000002521164644_d0e44409:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **HetuEngine** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
