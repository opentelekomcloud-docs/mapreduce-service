:original_name: ALM-50843.html

.. _ALM-50843:

ALM-50843 StoreWorker Node Communication Exception
==================================================

Alarm Description
-----------------

The system checks the failures of a StoreWorker node to send network messages on an instance every 10 minutes. This alarm is generated when the number of failures exceeds the threshold.

This alarm is cleared when the number of failures falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50843    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The network of the node is unavailable, and user services fail.

Possible Causes
---------------

-  The node is overloaded. As a result, the network communication times out, and messages fail to be sent.
-  The node is not correctly connected with other nodes. As a result, messages fail to be sent.

Handling Procedure
------------------

**Determine the network error type.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50843**.

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, the network automatically recovers, and no further action is required.
   -  If no, go to :ref:`3 <alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li491571611132>`.

#. .. _alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li491571611132:

   Choose **Cluster** > **Services** > **MemArtsStore** > **Instances**, click the StoreWorker instance for which the alarm is generated, click the **Chart** tab of the instance, and select **Pool Execution** from **Chart Category** on the left.

#. Check whether **Average Latency of StoreWorker Pool Operations on MPLog** is greater than 1 second.

   -  If yes, go to :ref:`5 <alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li849319546319>`.
   -  If no, go to :ref:`7 <alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li10360155511379>`.

**Reduce the service load.**

5. .. _alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li849319546319:

   Reduce the service load.

6. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li10360155511379>`.

**Collect fault information.**

7.  .. _alm-50843__en-us_topic_0000002520267259_en-us_topic_0000002157418396_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
