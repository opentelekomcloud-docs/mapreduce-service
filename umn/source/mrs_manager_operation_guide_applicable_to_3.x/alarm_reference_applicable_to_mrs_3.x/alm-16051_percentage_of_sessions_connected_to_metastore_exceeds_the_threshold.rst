:original_name: ALM-16051.html

.. _ALM-16051:

ALM-16051 Percentage of Sessions Connected to MetaStore Exceeds the Threshold
=============================================================================

Alarm Description
-----------------

The system checks the percentage of sessions connected to MetaStore to the maximum number of sessions allowed by MetaStore every 30 seconds. This alarm is generated when the percentage exceeds the threshold.

This alarm is cleared when the percentage of MetaStore sessions is less than or equal to the threshold.

This alarm applies to MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 16051                 | Critical (default threshold: 90%) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 80%)    |                       |
+-----------------------+-----------------------------------+-----------------------+

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
| Additional Information | Trigger condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

If this alarm is generated, sessions connected to MetaStore are too many. As a result, new connections cannot be set up.

Possible Causes
---------------

Too many clients are connected to MetaStore.

Handling Procedure
------------------

**Change the maximum number of MetaStore connections.**

#. On MRS Manager, choose **Cluster** > **Services** > **Hive**, click **Configuration** and then **All Configurations**.

#. In the **All Configurations** tab, search for **hive.metastore.server.max.threads** and check whether the value is the maximum **10000**.

   -  If yes, go to :ref:`6 <alm-16051__en-us_topic_0000001759357929_li19517422154756>`.
   -  If no, go to :ref:`3 <alm-16051__en-us_topic_0000001759357929_li15632114075420>`.

#. .. _alm-16051__en-us_topic_0000001759357929_li15632114075420:

   Change the value of **hive.metastore.server.max.threads** to **10000** and click **Save**.

#. Click **Instances**, select all MetaStore instances, and choose **More** > **Restart Instance**.

   .. important::

      During MetaStore instance restart, the instance cannot provide services for external systems. SQL tasks that are being executed on the instance may fail.

#. Check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-16051__en-us_topic_0000001759357929_li19517422154756>`.

**Collect fault information.**

6.  .. _alm-16051__en-us_topic_0000001759357929_li19517422154756:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Expand the **Service** drop-down list, and select **Hive** for the target cluster.

8.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9.  On MRS Manager, choose **Cluster** > **Services** > **Hive**. On the displayed **Dashboard** page, click **More** and select **Collect Stack Information**. On the displayed page, set the following parameters:

    -  Select **MetaStore** for the role where you want to collect data.
    -  Select **jstack** and **Enable continuous collection of jstack and jmap -histo information**.
    -  Set the collection interval to 10 seconds and the duration to 2 minutes.

10. Click **OK**. After the collection is complete, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
