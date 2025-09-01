:original_name: ALM-47004.html

.. _ALM-47004:

ALM-47004 Average Latency of MemArtsCC Worker Read Requests Exceeds the Threshold
=================================================================================

.. note::

   This section is available for MRS 3.5.0-LTS or later version only.

Alarm Description
-----------------

The system checks the average latency of all read requests to the MemArtsCC Worker process component every 30 seconds. This alarm is generated when the average latency exceeds the limit.

This alarm is cleared when the latency of MemArtsCC Worker read requests is lower than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
47004    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The cache performance may deteriorate.

Possible Causes
---------------

There is a soaring increase of concurrent requests sent by upper-layer computing services (such as Spark, Hive, and HetuEngine). Or, the service load or disk load increases significantly that even a fault occurs.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, search for **ALM-47004 Average Latency of MemArtsCC Worker Read Requests Exceeds the Threshold**, and locate the abnormal MemArtsCC instance node based on the alarm information. Obtain the alarm threshold in additional information.

#. On the **Alarms** page, check whether a disk fault alarm is generated.

   -  If yes, go to :ref:`3 <alm-47004__li9333108144418>`.
   -  If no, go to :ref:`4 <alm-47004__li1263992516714>`.

#. .. _alm-47004__li9333108144418:

   Contact O&M engineers to rectify the disk fault. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-47004__li16769101318212>`.

#. .. _alm-47004__li1263992516714:

   Ignore the alarm. Check whether the alarm is cleared when service load goes down.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-47004__li16769101318212>`.

**Collect fault information.**

5. .. _alm-47004__li16769101318212:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **MemArtsCC** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
