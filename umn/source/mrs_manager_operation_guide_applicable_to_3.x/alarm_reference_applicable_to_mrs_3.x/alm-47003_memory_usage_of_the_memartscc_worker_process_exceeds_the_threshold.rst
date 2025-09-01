:original_name: ALM-47003.html

.. _ALM-47003:

ALM-47003 Memory Usage of the MemArtsCC Worker Process Exceeds the Threshold
============================================================================

.. note::

   This section is available for MRS 3.5.0-LTS or later version only.

Alarm Description
-----------------

The system checks the memory usage of the CCWorker process of the MemArtsCC component every 30 seconds. This alarm is generated when the memory usage exceeds the threshold.

This alarm is cleared when the system detects that the memory usage of CCWorker process is lower than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
47003    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+-------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                       |
+======================+=============+===================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm is generated. |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm is generated.           |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm is generated.              |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm is generated.              |
+----------------------+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The CCWorker process process may restart, which temporarily reduces the cache hit ratio.

Possible Causes
---------------

There is more disk space added to CCWorker, there is a sudden increase in service data, or the workload increases significantly when upper-layer computing services (such as Spark, Hive, and HetuEngine) sent many concurrent requests to the MemArtsCC component.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, search for **ALM-47003 Memory Usage of the MemArtsCC Worker Process Exceeds the Threshold**, and locate the abnormal MemArtsCC instance node based on the alarm information. Obtain the alarm threshold in additional information.

#. .. _alm-47003__li1511344114716:

   Choose **Cluster** > **Services** > **MemArtsCC** > **Configurations** > **All Configurations** > **CCWorker (Role)**, search for the **memory_limit** parameter, and check the maximum available memory of the CCWorker instance in the current cluster. Check whether the service concurrency and data volume increase for a long time and the alarm is not automatically cleared.

   -  If yes, go to :ref:`4 <alm-47003__li14983142351220>`.
   -  If no, go to :ref:`3 <alm-47003__li1263992516714>`.

#. .. _alm-47003__li1263992516714:

   This alarm can be ignored temporarily. After the service peak hours, the alarm will be automatically cleared.

#. .. _alm-47003__li14983142351220:

   Increase the maximum available memory in :ref:`2 <alm-47003__li1511344114716>` and click Save.

#. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-47003__li16769101318212>`.

**Collect fault information.**

6. .. _alm-47003__li16769101318212:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **MemArtsCC** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
