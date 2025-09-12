:original_name: ALM-45007.html

.. _ALM-45007:

ALM-45007 Number of Workers of a HetuEngine Compute Instance Is Less Than the Threshold
=======================================================================================

This section applies to MRS 3.3.1 or later.

Alarm Description
-----------------

The system checks the number of Workers of a HetuEngine compute instance every 60 seconds. This alarm is generated when the number of Workers is less than 80% of the initial value.

This alarm is cleared when the number of Workers running on the HetuEngine compute instance is no less than 80% of the initial value.

Alarm Attributes

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45007    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
| Type                   | Parameter             | Description                                                                                                                |
+========================+=======================+============================================================================================================================+
| Location Information   | Source                | Specifies the cluster for which the alarm was generated.                                                                   |
+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | ServiceName           | Specifies the service for which the alarm was generated.                                                                   |
+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | RoleName              | Specifies the role for which the alarm was generated.                                                                      |
+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
|                        | HostName              | Specifies the host for which the alarm was generated.                                                                      |
+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
| Additional Information | Worker Less Threshold | Specifies the tenant name of the compute instance for which the alarm is generated and how much the threshold is exceeded. |
+------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The performance of the compute instance deteriorates and the SQL response becomes slow.

Possible Causes
---------------

-  YARN queue resources are insufficient.
-  A large number of tasks are running, causing OMM memory overflow on Worker nodes. As a result, the number of Worker nodes decreases.

Handling Procedure
------------------

**Check whether YARN resource queue resources are sufficient.**

#. Log in to MRS Manager as an administrator who can access the HetuEngine web UI.

#. Choose **O&M** > **Alarm** > **Alarms** > **Number of Workers of a HetuEngine Compute Instance Is Less Than the Threshold**, check the **Additional Information** of the alarm, and view and record the tenant name for which the alarm is generated.

#. Click **Tenant Resources**, select the tenant of the compute instance, and check whether the resource quota of the tenant is sufficient.

   -  If yes, go to :ref:`6 <alm-45007__li1779014615488>`.
   -  If no, go to :ref:`4 <alm-45007__li746891213395>`.

#. .. _alm-45007__li746891213395:

   Increase the maximum percentage of the tenant's resources based on the actual usage.

#. Wait 5 to 10 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45007__li1779014615488>`.

**Check whether there is a large number of running tasks.**

6.  .. _alm-45007__li1779014615488:

    Choose **Cluster** > **Services** > **HetuEngine**.

7.  In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole Web UI** to access the HSConsole page.

8.  On the **Compute Instances** page, expand the instances of the tenant and click **LINK** in the **WebUI** column of a compute instance to view the status of all tasks.

9.  Check whether the number of running tasks exceeds 50.

    -  If yes, go to :ref:`10 <alm-45007__li1846818125393>`.
    -  If no, go to :ref:`12 <alm-45007__li14468112103920>`.

10. .. _alm-45007__li1846818125393:

    Reduce the number of jobs submitted at a time or add compute instance resources based on service requirements.

11. Wait 5 to 10 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-45007__li14468112103920>`.

**Collect fault information.**

12. .. _alm-45007__li14468112103920:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

13. Expand the **Service** drop-down list, select **HetuEngine** for the target cluster, and click **OK**.

14. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

15. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
