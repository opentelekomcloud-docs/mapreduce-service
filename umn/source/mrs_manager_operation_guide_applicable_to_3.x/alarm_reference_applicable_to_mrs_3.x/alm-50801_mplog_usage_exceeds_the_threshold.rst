:original_name: ALM-50801.html

.. _ALM-50801:

ALM-50801 MPLog Usage Exceeds the Threshold
===========================================

Alarm Description
-----------------

The system checks the MPLog watermark of the StoreWorker component every 30 seconds. This alarm is generated when the MPLog watermark exceeds 100%.

This alarm is cleared when the watermark is lower than 100%.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50801    Minor          Yes
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

The node performance deteriorates.

Possible Causes
---------------

The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Change the watermark threshold.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **Pool Execution** > **MPLog Usage Level**.
#. Click |image1| next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

#. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.
#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50801__en-us_topic_0000002520267239_en-us_topic_0000002157418360_li2051913258201>`.

**Collect fault information.**

5. .. _alm-50801__en-us_topic_0000002520267239_en-us_topic_0000002157418360_li2051913258201:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002586673969.png
