:original_name: ALM-50402.html

.. _ALM-50402:

ALM-50402 JobGateway Service Unavailable
========================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the JobGateway service status every 60 seconds. This alarm is generated when the JobGateway service is abnormal.

This alarm is cleared when the JobGateway service recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50402    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+-------------------------------------------------------------------+
| Parameter   | Description                                                       |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

No job submission operation can be performed on JobGateway in the cluster. The components that depend on JobGateway in the cluster will become faulty.

Possible Causes
---------------

The node where the JobGateway service locates is faulty.

Handling Procedure
------------------

#. .. _alm-50402__li431925741816:

   Log in to FusionInsight Manager, choose **Cluster** > **Services** > **JobGateway**, and click the **Instance** tab. Check for JobServer or JobBalancer instances that are faulty or not started and view the host names of these instances.

#. On the **Alarm** page of FusionInsight Manager, check whether the **NodeAgent Process Is Abnormal** alarm is generated.

   -  If yes, go to :ref:`3 <alm-50402__li854418235198>`.
   -  If no, go to :ref:`6 <alm-50402__li2051913258201>`.

#. .. _alm-50402__li854418235198:

   Check whether the host name in the alarm information is the same as the host name in :ref:`1 <alm-50402__li431925741816>`.

   -  If yes, go to :ref:`4 <alm-50402__li952112310198>`.
   -  If no, go to :ref:`6 <alm-50402__li2051913258201>`.

#. .. _alm-50402__li952112310198:

   Clear the alarm by following the instructions provided in **ALM-12006 NodeAgent Process Is Abnormal**.

#. In the alarm list, check whether alarm **JobGateway Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-50402__li2051913258201>`.

**Collect fault information.**

6. .. _alm-50402__li2051913258201:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **JobGateway** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002007533201.png
