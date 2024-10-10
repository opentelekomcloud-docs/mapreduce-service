:original_name: ALM-50401.html

.. _ALM-50401:

ALM-50401 Number of JobServer Jobs Waiting to Be Executed Exceeds the Threshold
===============================================================================

.. note::

   This section applies only to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the number of jobs submitted to JobServer every 30 seconds. This alarm is generated when the number of jobs to be executed exceeds 800.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 50401                 | Critical (default threshold: 900) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 800)    |                       |
+-----------------------+-----------------------------------+-----------------------+

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

Too many JobServer jobs are detected in the queue. For details about the queue usage, see the **Additional Information** field of this alarm. The impacts are as follows:

#. When the number of JobServer jobs in the queue reaches the maximum (1000 by default), new jobs cannot be added.
#. Before the number of JobServer jobs in the queue reaches the maximum, new JobServer jobs cannot be submitted quickly. For example, it takes more time (even hours) to submit added jobs or add new jobs to Yarn.

Possible Causes
---------------

Too many jobs are submitted instantaneously.

Handling Procedure
------------------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **JobGateway**.
#. Click the **Instances** tab, click **Add Instance**, and add JobServer instances based on the number of submitted jobs.

3. After the instances are added, restart the JobGateway service.

   .. important::

      The job functions of JobGateway will become unavailable during the service restart.

4. Wait 5 minutes and check whether the alarm is automatically cleared.

   If yes, no further action is required.

   If no, go to :ref:`5 <alm-50401__li1559486215>`.

**Collect fault information.**

5. .. _alm-50401__li1559486215:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **JobGateway** for the target cluster.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000001971172618.png
