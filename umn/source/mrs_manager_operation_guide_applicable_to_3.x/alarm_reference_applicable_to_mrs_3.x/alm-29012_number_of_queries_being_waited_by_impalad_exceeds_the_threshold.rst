:original_name: ALM-29012.html

.. _ALM-29012:

ALM-29012 Number of Queries Being Waited by Impalad Exceeds the Threshold
=========================================================================

Alarm Description
-----------------

The system checks the total number of queries being waited by the Impalad node every 60 seconds. This alarm is generated when the number of queries exceeds the customized threshold (150 by default).

This alarm is automatically cleared when the number of queries is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
29012    Major          Yes
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

The queries may be blocked or even fail.

Possible Causes
---------------

The Impalad service has maintained a large number of queries, or the threshold is too small.

Handling Procedure
------------------

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds** > **Impala** > **Query Task Sum Statistics** > **Total number of Waiting Queries (Impalad)** and check the threshold.

   |image1|

#. Change the threshold.

   |image2|

#. Click the **Instances** tab, select all Impalad instances, and restart them.

   .. note::

      The service will become unavailable when all instances are restarted. If a single instance is restarted, the tasks that are being executed on that instance will fail and the service will become available.

   |image3|

4. After the restart is complete, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-29012__li17918612154249>`.

**Collect fault information.**

5. .. _alm-29012__li17918612154249:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Impala** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001971010174.png
.. |image2| image:: /_static/images/en-us_image_0000002007530505.png
.. |image3| image:: /_static/images/en-us_image_0000002007650001.png
