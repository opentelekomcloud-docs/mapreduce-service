:original_name: ALM-45743.html

.. _ALM-45743:

ALM-45743 Failed to Call the IAM API
====================================

Alarm Description
-----------------

This alarm is generated when Guardian fails to call the IAM API to obtain a temporary AK/SK.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45743    Major          Yes
======== ============== ============

Alarm Parameters
----------------

=========== ========================================================
Parameter   Description
=========== ========================================================
Source      Specifies the cluster for which the alarm was generated.
ServiceName Specifies the service for which the alarm was generated.
RoleName    Specifies the role for which the alarm was generated.
HostName    Specifies the host for which the alarm was generated.
=========== ========================================================

Impact on the System
--------------------

The task may fail to obtain the temporary AK/SK for accessing OBS. As a result, the task cannot access OBS.

Possible Causes
---------------

The IAM service is abnormal.

Handling Procedure
------------------

**Collect fault information.**

#. On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.
#. Expand the **Service** drop-down list, and select **Guardian** for the target cluster.
#. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.
#. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002008222021.png
