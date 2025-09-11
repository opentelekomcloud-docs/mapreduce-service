:original_name: ALM-45006.html

.. _ALM-45006:

ALM-45006 Memory Usage of a HetuEngine Compute Instance Exceeded the Threshold
==============================================================================

This section applies to MRS 3.3.1 or later.

Alarm Description
-----------------

The system checks the memory usage of HetuEngine compute instances every 30 seconds. This alarm is generated when the memory usage of the instance is greater than 80%.

This alarm is cleared when the memory usage of the HetuEngine compute instance is no more than 80%.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45006    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Type                   | Parameter                          | Description                                                                                                                |
+========================+====================================+============================================================================================================================+
| Location Information   | Source                             | Specifies the cluster for which the alarm was generated.                                                                   |
+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | ServiceName                        | Specifies the service for which the alarm was generated.                                                                   |
+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | RoleName                           | Specifies the role for which the alarm was generated.                                                                      |
+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | HostName                           | Specifies the host for which the alarm was generated.                                                                      |
+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Additional Information | Memory Usage Exceeds The Threshold | Specifies the tenant name of the compute instance for which the alarm is generated and how much the threshold is exceeded. |
+------------------------+------------------------------------+----------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The performance of the compute instance deteriorates and the response to service SQL statements becomes slow.

Possible Causes
---------------

-  The compute instance specification is too small.
-  Large SQL tasks occupy too many compute resources. No resource is available for other tasks, and the compute instance cannot respond quickly. As a result, tasks are stacked.

Handling Procedure
------------------

**Check whether compute instance resources are properly configured.**

#. Log in to MRS Manager as an administrator who can access the HetuEngine web UI.

#. Choose **O&M** > **Alarm** > **Alarms** > **Tasks Stacked on HetuEngine Compute Instance**, check the **Additional Information** of the alarm, and view and record the tenant name for which the alarm is generated.

#. Choose **Cluster** > **Services** > HetuEngine. In the **Basic Information** area in the **Dashboard** tab, click the link next to **HSConsole Web UI**. The HSConsole page is displayed.

#. On the **Compute Instance** page, click **Configure** in the **Operation** column of the tenant to which the compute instance belongs. Check whether the resource configured for the compute instance is proper. (The the minimum resources are used by default. You can adjust the configuration based on the site requirements.)

   -  If yes, go to :ref:`8 <alm-45006__en-us_topic_0000001849713901_li1561212104442>`.
   -  If no, go to :ref:`5 <alm-45006__en-us_topic_0000001849713901_li7562123964615>`.

#. .. _alm-45006__en-us_topic_0000001849713901_li7562123964615:

   Return to the compute instance list, click **Stop Instances** in the **Operation** column, and stop instances as prompted.

   .. important::

      Tasks submitted to the stopped compute instances will be interrupted.

#. Click **Configure**, add resources to the target compute instance based on the site requirements, and click **OK**. Click **Start Instances** and start instances as prompted.

#. Wait 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45006__en-us_topic_0000001849713901_li1561212104442>`.

**Check whether there are large SQL tasks.**

8.  .. _alm-45006__en-us_topic_0000001849713901_li1561212104442:

    On the **Compute Instances** page, expand the instances of the tenant and click **LINK** in the **WebUI** column of a compute instance to view the status of all tasks.

9.  In the **Sort** column, select **Execution Time** to sort the running tasks and check whether there are tasks that have been running for hours.

    -  If yes, go to :ref:`10 <alm-45006__en-us_topic_0000001849713901_li1266819163911>`.
    -  If no, go to :ref:`12 <alm-45006__en-us_topic_0000001849713901_li1573581113104>`.

10. .. _alm-45006__en-us_topic_0000001849713901_li1266819163911:

    End the tasks that have been running for a long time based on service requirement and optimize the service SQL statements.

11. Wait 2 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-45006__en-us_topic_0000001849713901_li1573581113104>`.

**Collect fault information.**

12. .. _alm-45006__en-us_topic_0000001849713901_li1573581113104:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

13. Expand the **Service** drop-down list, select **HetuEngine** for the target cluster, and click **OK**.

14. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

15. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M engineers and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
