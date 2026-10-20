:original_name: ALM-45012.html

.. _ALM-45012:

ALM-45012 HSFabric GC Duration Exceeds the Threshold
====================================================

Alarm Description
-----------------

The system checks the garbage collection (GC) duration of the HSFabric process every 60 seconds. This alarm is generated when the GC duration of the HSFabric process exceeds the threshold (12,000 ms by default) for three consecutive times.

This alarm is automatically cleared when the system detects that the GC duration is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45012    Major          No
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

HSFabric may respond slowly and the access to the HSFabric may be interrupted.

Possible Causes
---------------

The heap memory of the HSFabric process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Handling Procedure
------------------

**Check the GC duration of the HSFabric process.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45012 HSFabric GC Duration Exceeds the Threshold**. In the **Location** field of the alarm details, check the instance host name for which the alarm is generated.

#. .. _alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_li43047473:

   Choose **Cluster** > **Services** > **HetuEngine** > **Instances** and click the instance host name for which the alarm is generated. Click the drop-down list in the upper right corner of the chart area, choose **Customize** > **GC** > **GC Duration of the HSFabric Process**, and click **OK**.

#. Check whether the GC duration of the HSFabric process collected every minute exceeds the threshold (12,000 ms by default).

   -  If yes, go to :ref:`4 <alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_d0e44388>`.
   -  If no, go to :ref:`6 <alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_d0e44409>`.

#. .. _alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_d0e44388:

   Choose **Cluster** > **Services** > **HetuEngine** > **Instances** > **HSFabric** > **Instance Configurations** > **All Configurations**, and select **HSFabric** > **Tuning**. Set **-Xmx** in the **GC_OPTS** parameter to a larger value based on site requirements and save the configuration.

   .. note::

      If this alarm is generated, the heap memory configured for HSFabric cannot meet the heap memory required by the HSFabric process. You are advised to change the value of **-Xmx** in **GC_OPTS** to the twice that of the heap memory used by HSFabric. You can change the value based on the actual service scenario. For details about how to check the HSFabric heap memory usage, see :ref:`2 <alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_li43047473>`.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_d0e44409>`.

   .. caution::

      During the restart of the service or instance, HSFabric may fail to be accessed.

**Collect fault information.**

6. .. _alm-45012__en-us_topic_0000002524106028_en-us_topic_0000002552244623_d0e44409:

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
