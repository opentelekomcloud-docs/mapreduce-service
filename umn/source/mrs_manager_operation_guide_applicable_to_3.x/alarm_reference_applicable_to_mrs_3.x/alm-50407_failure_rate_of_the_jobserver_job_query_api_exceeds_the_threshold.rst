:original_name: ALM-50407.html

.. _ALM-50407:

ALM-50407 Failure Rate of the JobServer Job Query API Exceeds the Threshold
===========================================================================

.. note::

   This section is available for MRS 3.5.0-LTS or later version only.

Alarm Description
-----------------

The system checks the failure rate of the JobServer job query API every 30 seconds. This alarm is generated when the failure rate exceeds the threshold (80% by default).

This alarm is cleared when the failure rate falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50407    Critical       Yes
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

A job may fail to be queried, for example, through the REST API.

Possible Causes
---------------

The JobServer instance on the node is abnormal.

Handling Procedure
------------------

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, expand details of this alarm in the right pane, and obtain **HostName** of the node for which the alarm is generated in **Location**.

2. On MRS Manager, choose **Cluster** > **Services** > **JobGateway** > **Instances**.

3. Select the instance for which the alarm is generated, click **More**, and select **Instance Rolling Restart**.

   .. note::

      Services may be affected or interrupted during the restart. You are advised to perform the restart during off-peak hours.

4. Check whether the instance running status is normal after the restart.

   -  If yes, go to :ref:`5 <alm-50407__li50867023154840>`.
   -  If no, go to :ref:`6 <alm-50407__li1559486215>`.

5. .. _alm-50407__li50867023154840:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-50407__li1559486215>`.

**Collect fault information.**

6. .. _alm-50407__li1559486215:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **JobGateway** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002381782678.png
