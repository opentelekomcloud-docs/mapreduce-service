:original_name: ALM-45182.html

.. _ALM-45182:

ALM-45182 Number of Throttled OBS Operations Exceeds the Threshold
==================================================================

Description
-----------

The system checks whether the number of throttled OBS operations exceeds the threshold every 30 seconds. This alarm is generated when the number of throttled OBS operations exceeds the threshold.

This alarm is automatically cleared when the number of throttled OBS operations is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45182    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Certain upper-layer big data computing tasks will fail to execute.

Possible Causes
---------------

The frequency of requesting OBS APIs is too high.

Procedure
---------

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds**. On the **Thresholds** page, choose **meta** > **Number of Throttled OBS Operations**. In the right pane, set **Threshold** or **Trigger Count** to a larger value as required.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-45182__li1689719391331>`.

#. .. _alm-45182__li1689719391331:

   Contact OBS O&M personnel to check whether the OBS service is normal.

   -  If yes, go to :ref:`4 <alm-45182__li19825189163317>`.
   -  If no, contact OBS O&M personnel to restore the OBS service.

**Collect fault information.**

4. .. _alm-45182__li19825189163317:

   On MRS Manager, choose **Cluster** > **Services** > **meta**. On the page that is displayed, click the **Chart** tab. On this tab page, select **OBS Throttled** in the **Chart Category** area. In the **Number of Throttled OBS Operations-All Instances** chart, view the host name of the instance that has the maximum number of throttled OBS API calls. For example, the host name is **node-ana-coreUQqJ0002**.

   |image1|

5. Choose **O&M** > **Log** > **Download** and select **meta** and **meta** under it for **Service**.

6. Select the host obtained in :ref:`4 <alm-45182__li19825189163317>` for **Hosts**.

7. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.
8. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087453.png
.. |image2| image:: /_static/images/en-us_image_0000001532607802.png
