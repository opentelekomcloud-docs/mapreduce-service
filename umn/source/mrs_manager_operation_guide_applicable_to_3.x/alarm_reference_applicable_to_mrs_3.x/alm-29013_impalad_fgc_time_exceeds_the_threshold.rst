:original_name: ALM-29013.html

.. _ALM-29013:

ALM-29013 Impalad FGC Time Exceeds the Threshold
================================================

Alarm Description
-----------------

The system checks the FGC time of the Impalad service every 60 seconds. This alarm is generated when the FGC time exceeds the threshold (12 seconds) for five consecutive times. This alarm is cleared when the FGC time is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
29013    Major          Yes
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
| Additional Information | Trigger Condition | Specifies the threshold for triggering the alarm.        |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Data read and write are affected.

Possible Causes
---------------

The memory of the node instance is overused or the heap memory is inappropriately allocated, causing frequent occurrence of the GC process.

Handling Procedure
------------------

**Check the GC time.**

#. .. _alm-29013__li2072324101912:

   Choose **O&M** > **Alarm** > **Thresholds** > **Impala** > **Process FGCT** > **Process FGCT of Impalad (Impalad)**, and check the threshold (12s by default).

   |image1|

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether the alarm whose **Alarm ID** is **29013** exists in the alarm list.

   -  If yes, go to :ref:`3 <alm-29013__li972417412195>`.
   -  If no, no further action is required.

#. .. _alm-29013__li972417412195:

   On FusionInsight Manager, choose **Cluster** > **Impala**, click the **Instances** tab, select the Impalad instance for which the alarm is generated, then click the **Chart** tab, locate the **Process FGCT** chart, and check whether the FGC time is greater than the threshold in :ref:`1 <alm-29013__li2072324101912>`.

   -  If yes, go to :ref:`4 <alm-29013__li16724841191916>`.
   -  If no, go to :ref:`5 <alm-29013__li188852383514>`.

#. .. _alm-29013__li16724841191916:

   Choose **O&M** > **Alarm** > **Thresholds** > **Impala** > **Process FGCT** > **Process FGCT of Impalad (Impalad)**, and change the threshold to a value less than the time obtained in :ref:`3 <alm-29013__li972417412195>`. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-29013__li188852383514>`.

**Collect fault information.**

5. .. _alm-29013__li188852383514:

   On FusionInsight Manager of the active or standby cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Impala** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001971169962.png
