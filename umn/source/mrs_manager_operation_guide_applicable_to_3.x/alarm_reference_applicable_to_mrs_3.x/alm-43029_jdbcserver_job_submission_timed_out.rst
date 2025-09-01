:original_name: ALM-43029.html

.. _ALM-43029:

ALM-43029 JDBCServer Job Submission Timed Out
=============================================

.. note::

   This section applies only to MRS 3.5.0-LTS or later.

Alarm Description
-----------------

After a user submits a JDBC job, the system attempts to create a JDBCServer process and establish a session connection. This alarm is generated if the preset thresholds are exceeded before the connection is established. There are two configuration parameters affecting alarm triggering:

-  **spark.thriftserver.proxy.create.session.monitor.enabled**: whether to enable the alarm function. The default value is **true** for the cluster.
-  **spark.thriftserver.proxy.create.session.timeout.threshold**: Maximum time allowed for submitting a JDBC job. This alarm is reported when the system detects that the job does not start after the threshold is exceeded. The unit is second. The default value is 180s.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
43029    Major          No
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------+----------------------------------------------------------------------------------------+
| Type                   | Parameter   | Description                                                                            |
+========================+=============+========================================================================================+
| Location Information   | Source      | Specifies the cluster for which the alarm was generated.                               |
+------------------------+-------------+----------------------------------------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated.                               |
+------------------------+-------------+----------------------------------------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.                                  |
+------------------------+-------------+----------------------------------------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.                                  |
+------------------------+-------------+----------------------------------------------------------------------------------------+
| Additional Information | User_Queue  | Name of the user who submits the alarm and the queue for which the alarm is generated. |
+------------------------+-------------+----------------------------------------------------------------------------------------+

Impact on the System
--------------------

The JDBC job submission time increases due to high system load, which may also affect the job execution efficiency. The job can start properly after this alarm is reported because the detection is asynchronous.

Possible Causes
---------------

The JDBCServer on the node is overloaded. The cluster health reflected by the system metrics and job execution status is not good.

Handling Procedure
------------------

**Check the JDBCServer instance for which the alarm is generated.**

#. On MRS Manager, choose O&M > Alarm > Alarms and select the alarm whose ID is 43029. Check the role name and the IP address of the host where the alarm is generated in **Location**. Check the username and queue in **Additional Information**.

**Re-executing Affected JDBCServer Jobs**

2. Choose **Cluster** > **Services** > **Yarn** > **ResourceManager (Active)** to log in to the YARN web UI. Find the corresponding application based on the username and queue name in **Additional Information** and check whether the job submission is affected based on the driver log and Spark UI. Confirm and record the affected job to execute it again.
3. On MRS Manager, choose **Cluster** > **Services** > **Spark** > **Instances**, click the JDBCServer for which this alarm is generated, and choose **More** > **Restart Instance**.
4. Choose **O&M** > **Alarm** > **Alarms**, search for the reported alarm, and click **Clear** in the **Operation** column.
5. Execute the affected job and check whether the alarm is triggered again for the job.

   -  If no, no further action is required.
   -  If yes, go to :ref:`6 <alm-43029__li79972052174314>`.

**Collect fault information.**

6. .. _alm-43029__li79972052174314:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Spark** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm needs to be cleared manually.

Related Information
-------------------

None.
