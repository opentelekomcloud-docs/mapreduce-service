:original_name: ALM-50844.html

.. _ALM-50844:

ALM-50844 StoreMaster Node Communication Exception
==================================================

Alarm Description
-----------------

The system checks the failures of a StoreMaster node to send network messages on an instance every 10 minutes. This alarm is generated when the number of failures exceeds the threshold.

This alarm is cleared when the number of failures falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50844    Major          Yes
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

The node is not correctly connected with other nodes. As a result, messages fail to be sent.

Handling Procedure
------------------

**Determine the network error type.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50844**.

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, the network automatically recovers, and no further action is required.
   -  If no, go to :ref:`3 <alm-50844__en-us_topic_0000002488107414_en-us_topic_0000002192819545_li491571611132>`.

#. .. _alm-50844__en-us_topic_0000002488107414_en-us_topic_0000002192819545_li491571611132:

   Select the instance for which the alarm is generated, click **More**, and select **Restart Instance**. In the dialog box that is displayed, enter the password, and click **OK** to restart the StoreMaster instance.

4. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50844__en-us_topic_0000002488107414_en-us_topic_0000002192819545_li10360155511379>`.

**Collect fault information.**

5. .. _alm-50844__en-us_topic_0000002488107414_en-us_topic_0000002192819545_li10360155511379:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
