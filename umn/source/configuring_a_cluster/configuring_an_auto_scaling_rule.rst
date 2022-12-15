:original_name: mrs_01_0061.html

.. _mrs_01_0061:

Configuring an Auto Scaling Rule
================================

Background
----------

In big data application scenarios, especially real-time data analysis and processing, the number of cluster nodes needs to be dynamically adjusted according to data volume changes to provide the required number of resources. The auto scaling function of MRS enables the task nodes of a cluster to be automatically scaled to match cluster loads. If the data volume changes periodically, you can configure an auto scaling rule so that the number of task nodes can be automatically adjusted in a fixed period of time before the data volume changes.

-  Auto scaling rules: You can increase or decrease task nodes based on real-time cluster loads. Auto scaling will be triggered with a certain delay when the data volume changes.
-  Resource plans: Set the task node quantity based on the time range. If the data volume changes periodically, you can create resource plans to resize the cluster before the data volume changes, thereby avoiding delays in increasing or decreasing resources.

You can configure either auto scaling rules or resource plans or both to trigger auto scaling. Configuring both resource plans and auto scaling rules improves the cluster node scalability to cope with occasionally unexpected data volume peaks.

In some service scenarios, resources need to be reallocated or service logic needs to be modified after cluster scale-out or scale-in. If you manually scale out or scale in a cluster, you can log in to cluster nodes to reallocate resources or modify service logic. If you use auto scaling, MRS enables you to customize automation scripts for resource reallocation and service logic modification. Automation scripts can be executed before and after auto scaling and automatically adapt to service load changes, all of which eliminates manual operations. In addition, automation scripts can be fully customized and executed at various moments, meeting your personalized requirements and improving auto scaling flexibility.

-  Auto scaling rules:

   -  You can set a maximum of five rules for scaling out or in a cluster, respectively.
   -  The system determines the scale-out and then scale-in based on your configuration sequence. Important policies take precedence over other policies to prevent repeated triggering when the expected effect cannot be achieved after a scale-out or scale-in.
   -  Comparison factors include greater than, greater than or equal to, less than, and less than or equal to.
   -  Cluster scale-out or scale-in can be triggered only after the configured metric threshold is reached for consecutive 5\ *n* (the default value of *n* is 1) minutes.
   -  After each scale-out or scale-in, there is a cooling duration is greater than 0, and lasts 20 minutes by defaults.
   -  In each cluster scale-out or scale-in, at least one node and at most 100 nodes can be added or reduced.

-  Resource plans (setting the number of Task nodes by time range):

   -  You can specify a Task node range (minimum number to maximum number) in a time range. If the number of Task nodes is beyond the Task node range in a resource plan, the system triggers cluster scale-out or scale-in.
   -  You can set a maximum of five resource plans for a cluster.
   -  A resource plan cycle is by day. The start time and end time can be set to any time point between 00:00 and 23:59. The start time must be at least 30 minutes earlier than the end time. Time ranges configured for different resource plans cannot overlap.
   -  After a resource plan triggers cluster scale-out or scale-in, there is 10-minute cooling duration. Auto scaling will not be triggered again within the cooling time.
   -  When a resource plan is enabled, the number of Task nodes in the cluster is limited to the default node range configured by you in other time periods except the time period configured in the resource plan.
   -  If the resource plan is not enabled, the number of Task nodes is not limited to the default node range.

-  Automation scripts:

   -  You can set an automation script so that it can automatically run on cluster nodes when auto scaling is triggered.
   -  You can set a maximum number of 10 automation scripts for a cluster.
   -  You can specify an automation script to be executed on one or more types of nodes.
   -  Automation scripts can be executed before or after scale-out or scale-in.
   -  Before using automation scripts, upload them to a cluster VM or OBS file system in the same region as the cluster. The automation scripts uploaded to the cluster VM can be executed only on the existing nodes. If you want to make the automation scripts run on the new nodes, upload them to the OBS file system.

Accessing the Auto Scaling Configuration Page
---------------------------------------------

You can configure an auto scaling rule on the **Set Advanced Options** page during cluster creation or on the **Nodes** page after the cluster is created.

**Configuring an auto scaling rule when creating a cluster**

#. Log in to the MRS console.

#. When you create a cluster containing task nodes, configure the cluster software and hardware information by referring to :ref:`Creating a Custom Cluster <mrs_01_0513>`. Then, on the **Set Advanced Options** page, enable **Analysis Task** and configure or modify auto scaling rules and resource plans.

   You can configure the auto scaling rules by referring to the following scenarios:

   -  :ref:`Scenario 1: Using Auto Scaling Rules Alone <mrs_01_0061__section15610431184420>`
   -  :ref:`Scenario 2: Using Resource Plans Alone <mrs_01_0061__section1127519214291>`
   -  :ref:`Scenario 3: Using Both Auto Scaling Rules and Resource Plans <mrs_01_0061__section10800203113299>`

**Configure an auto scaling rule for an existing cluster**

#. Log in to the MRS console.

#. In the navigation pane on the left, choose **Clusters** > **Active Clusters** and click the name of a running cluster to go to the cluster details page.

#. Click the **Nodes** tab and then **Auto Scaling** in the **Operation** column of the task node group. The **Auto Scaling** page is displayed.

   .. note::

      -  If no task node exists in the cluster, click **Configure Task Node** to add one and then configure the auto scaling rules.
      -  For MRS 3.\ *x* or later, **Configure Task Node** is available only for analysis clusters, streaming clusters, and hybrid clusters. For details about how to add a task node for a custom cluster of MRS 3.\ *x* or later, see :ref:`Adding a Task Node <mrs_01_0041__section1077318341361>`.

#. Enable **Auto Scaling** and configure or modify auto scaling rules and resource plans.

   You can configure the auto scaling rules by referring to the following scenarios:

   -  :ref:`Scenario 1: Using Auto Scaling Rules Alone <mrs_01_0061__section15610431184420>`
   -  :ref:`Scenario 2: Using Resource Plans Alone <mrs_01_0061__section1127519214291>`
   -  :ref:`Scenario 3: Using Both Auto Scaling Rules and Resource Plans <mrs_01_0061__section10800203113299>`

.. _mrs_01_0061__section15610431184420:

Scenario 1: Using Auto Scaling Rules Alone
------------------------------------------

The following is an example scenario:

The number of nodes needs to be dynamically adjusted based on the Yarn resource usage. When the memory available for Yarn is less than 20% of the total memory, five nodes need to be added. When the memory available for Yarn is greater than 70% of the total memory, five nodes need to be removed. The number of nodes in a task node group ranges from 1 to 10.

#. Go to the **Auto Scaling** page to configure auto scaling rules.

   -  Configure the **Default Range** parameter.

      Enter a task node range, in which auto scaling is performed. This constraint applies to all scale-in and scale-out rules. The maximum value range allowed is 0 to 500.

      The value range in this example is 1 to 10.

   -  Configure an auto scaling rule.

      To enable **Auto Scaling**, you must configure a scale-out or scale-in rule.

      a. Select **Scale-Out** or **Scale-In**.

      b. Click **Add Rule**.

      c. Configure the **Rule Name**, **If**, **Last for**, **Add**, and **Cooldown Period** parameters.

      d. Click **OK**.

         You can view, edit, or delete the rules you configured in the **Scale-out** or **Scale-in** area on the **Auto Scaling** page. You can click **Add Rule** to configure multiple rules.

#. (Optional) Configure automation scripts.

   Set **Advanced Settings** to **Configure** and click **Created**, or click **Add Automation Script** to go to the **Automation Script** page.

   MRS 3.\ *x* does not support this operation.

   a. Set the following parameters: **Name**, **Script Path**, **Execution Node**, **Parameter**, **Executed**, and **Action upon Failure**. For details about the parameters, see :ref:`Table 4 <mrs_01_0061__table15644113520578>`.
   b. Click **OK** to save the automation script configurations.

#. Click **OK**.

   .. note::

      If you want to configure an auto scaling rule for an existing cluster, select **I agree to authorize MRS to scale out or in nodes based on the above rule**.

.. _mrs_01_0061__section1127519214291:

Scenario 2: Using Resource Plans Alone
--------------------------------------

If the data volume changes regularly every day and you want to scale out or in a cluster before the data volume changes, you can create resource plans to adjust the number of Task nodes as planned in the specified time range.

Example:

A real-time processing service sees a sharp increase in data volume from 7:00 to 13:00 every day. Assume that an MRS streaming cluster is used to process the service data. Five task nodes are required from 7:00 to 13:00, while only two are required at other time.

#. Go to the **Auto Scaling** page to configure a resource plan.

   a. For example, the **Default Range** is set to **2-2**, indicating that the number of Task nodes is fixed to 2 except the time range specified in the resource plan.

   b. Click **Configure Node Range for Specific Time Range** under **Default Range** or **Add Resource Plan**.

   c. Configure **Time Range** and **Node Range**.

      For example, set **Time Range** to **07:00-13:00**, and **Node Range** to **5-5**. This indicates that the number of task nodes is fixed at 5 from 07:00 to 13:00.

      For details about parameter configurations, see :ref:`Table 3 <mrs_01_0061__table1846575414619>`. You can click **Configure Node Range for Specific Time Range** to configure multiple resource plans.

      .. note::

         -  If you do not set **Node Range**, its default value will be used.
         -  If you set both **Node Range** and **Time Rang**\ e, the node range you set will be used during the time range you set, and the default node range will be used beyond the time range you set. If the time is not within the configured time range, the default range is used.

#. (Optional) Configure automation scripts.

   Set **Advanced Settings** to **Configure** and click **Created**, or click **Add Automation Script** to go to the **Automation Script** page.

   MRS 3.\ *x* does not support this operation.

   a. Set the following parameters: **Name**, **Script Path**, **Execution Node**, **Parameter**, **Executed**, and **Action upon Failure**. For details about the parameters, see :ref:`Table 4 <mrs_01_0061__table15644113520578>`.
   b. Click **OK** to save the automation script configurations.

#. Click **OK**.

   .. note::

      If you want to configure an auto scaling rule for an existing cluster, select **I agree to authorize MRS to scale out or in nodes based on the above rule**.

.. _mrs_01_0061__section10800203113299:

Scenario 3: Using Both Auto Scaling Rules and Resource Plans
------------------------------------------------------------

If the data volume is not stable and the expected fluctuation may occur, the fixed Task node range cannot guarantee that the requirements in some service scenarios are met. In this case, it is necessary to adjust the number of Task nodes based on the real-time loads and resource plans.

The following is an example scenario:

A real-time processing service sees an unstable increase in data volume from 7:00 to 13:00 every day. For example, 5 to 8 task nodes are required from 7:00 to 13:00, and 2 to 4 are required beyond this period. Therefore, you can set an auto scaling rule based on a resource plan. When the data volume exceeds the expected value, the number of Task nodes can be adjusted if resource loads change, without exceeding the node range specified in the resource plan. When a resource plan is triggered, the number of nodes is adjusted within the specified node range with minimum affect. That is, increase nodes to the upper limit and decrease nodes to the lower limit.

#. Go to the **Auto Scaling** page to configure auto scaling rules.

   -  **Default Range**

      Enter a task node range, in which auto scaling is performed. This constraint applies to all scale-in and scale-out rules.

      For example, this parameter is set to **2-4** in this scenario.

   -  **Auto Scaling**

      To enable **Auto Scaling**, you must configure a scale-out or scale-in rule.

      a. Select **Scale-Out** or **Scale-In**.

      b. Click **Add Rule**. The **Add Rule** page is displayed.

      c. Configure the **Rule Name**, **If**, **Last for**, **Add**, and **Cooldown Period** parameters.

      d. Click **OK**.

         You can view, edit, or delete the rules you configured in the **Scale-out** or **Scale-in** area on the **Auto Scaling** page.

#. Configure a resource plan.

   a. Click **Configure Node Range for Specific Time Range** under **Default Range** or **Add Resource Plan**.

   b. Configure **Time Range** and **Node Range**.

      For example, **Time Range** is set to **07:00-13:00** and **Node Range** to **5-8**.

      For details about parameter configurations, see :ref:`Table 3 <mrs_01_0061__table1846575414619>`. You can click **Configure Node Range for Specific Time Range** or **Add Resource Plan** to configure multiple resource plans.

      .. note::

         -  If you do not set **Node Range**, its default value will be used.
         -  If you set both **Node Range** and **Time Rang**\ e, the node range you set will be used during the time range you set, and the default node range will be used beyond the time range you set. If the time is not within the configured time range, the default range is used.

#. (Optional) Configure automation scripts.

   Set **Advanced Settings** to **Configure** and click **Created**, or click **Add Automation Script** to go to the **Automation Script** page.

   MRS 3.\ *x* does not support this operation.

   a. Set the following parameters: **Name**, **Script Path**, **Execution Node**, **Parameter**, **Executed**, and **Action upon Failure**. For details about the parameters, see :ref:`Table 4 <mrs_01_0061__table15644113520578>`.
   b. Click **OK** to save the automation script configurations.

#. Click **OK**.

   .. note::

      If you want to configure an auto scaling rule for an existing cluster, select **I agree to authorize MRS to scale out or in nodes based on the above rule**.

Related Information
-------------------

When adding a rule, you can refer to :ref:`Table 1 <mrs_01_0061__table15133845184415>` to configure the corresponding metrics.

.. _mrs_01_0061__table15133845184415:

.. table:: **Table 1** Auto scaling metrics

   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Cluster Type      | Metric                                   | Value Type      | Description                                                                                                  |
   +===================+==========================================+=================+==============================================================================================================+
   | Streaming cluster | StormSlotAvailable                       | Integer         | Number of available Storm slots                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotAvailablePercentage             | Percentage      | Percentage of available Storm slots, that is, the proportion of the available slots to total slots           |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsed                            | Integer         | Number of the used Storm slots                                                                               |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsedPercentage                  | Percentage      | Percentage of the used Storm slots, that is, the proportion of the used slots to total slots                 |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsage           | Integer         | Average memory usage of the Supervisor process of Storm                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsagePercentage | Percentage      | Average percentage of the used memory of the Supervisor process of Storm to the total memory of the system   |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorCPUAverageUsagePercentage | Percentage      | Average percentage of the used CPUs of the Supervisor process of Storm to the total CPUs                     |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 6000                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Analysis cluster  | YARNAppPending                           | Integer         | Number of pending tasks on YARN                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppPendingRatio                      | Ratio           | Ratio of pending tasks on Yarn, that is, the ratio of pending tasks to running tasks on Yarn                 |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppRunning                           | Integer         | Number of running tasks on Yarn                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerAllocated                   | Integer         | Number of containers allocated to Yarn                                                                       |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPending                     | Integer         | Number of pending containers on Yarn                                                                         |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPendingRatio                | Ratio           | Ratio of pending containers on Yarn, that is, the ratio of pending containers to running containers on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAllocated                         | Integer         | Number of virtual CPUs (vCPUs) allocated to Yarn                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailable                         | Integer         | Number of available vCPUs on Yarn                                                                            |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailablePercentage               | Percentage      | Percentage of available vCPUs on Yarn, that is, the proportion of available vCPUs to total vCPUs             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUPending                           | Integer         | Number of pending vCPUs on Yarn                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAllocated                      | Integer         | Memory allocated to Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailable                      | Integer         | Available memory on Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailablePercentage            | Percentage      | Percentage of available memory on Yarn, that is, the proportion of available memory to total memory on Yarn  |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryPending                        | Integer         | Pending memory on Yarn                                                                                       |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+

.. _mrs_01_0061__table12336184610200:

.. table:: **Table 2** Auto scaling metrics

   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Cluster Type    | Metric                                   | Value Type      | Description                                                                                                  |
   +=================+==========================================+=================+==============================================================================================================+
   | Custom          | StormSlotAvailable                       | Integer         | Number of available Storm slots                                                                              |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSlotAvailablePercentage             | Percentage      | Percentage of available Storm slots, that is, the proportion of the available slots to total slots           |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 100                                                                                        |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSlotUsed                            | Integer         | Number of the used Storm slots                                                                               |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSlotUsedPercentage                  | Percentage      | Percentage of the used Storm slots, that is, the proportion of the used slots to total slots                 |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 100                                                                                        |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSupervisorMemAverageUsage           | Integer         | Average memory usage of the Supervisor process of Storm                                                      |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSupervisorMemAverageUsagePercentage | Percentage      | Average percentage of the used memory of the Supervisor process of Storm to the total memory of the system   |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 100                                                                                        |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | StormSupervisorCPUAverageUsagePercentage | Percentage      | Average percentage of the used CPUs of the Supervisor process of Storm to the total CPUs                     |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 6000.                                                                                      |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNAppPending                           | Integer         | Number of pending tasks on YARN                                                                              |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNAppPendingRatio                      | Ratio           | Ratio of pending tasks on Yarn, that is, the ratio of pending tasks to running tasks on Yarn                 |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNAppRunning                           | Integer         | Number of running tasks on Yarn                                                                              |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNContainerAllocated                   | Integer         | Number of containers allocated to Yarn                                                                       |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNContainerPending                     | Integer         | Number of pending containers on Yarn                                                                         |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNContainerPendingRatio                | Ratio           | Ratio of pending containers on Yarn, that is, the ratio of pending containers to running containers on Yarn. |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNCPUAllocated                         | Integer         | Number of virtual CPUs (vCPUs) allocated to Yarn                                                             |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNCPUAvailable                         | Integer         | Number of available vCPUs on Yarn                                                                            |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNCPUAvailablePercentage               | Percentage      | Percentage of available vCPUs on Yarn, that is, the proportion of available vCPUs to total vCPUs             |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 100                                                                                        |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNCPUPending                           | Integer         | Number of pending vCPUs on Yarn                                                                              |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNMemoryAllocated                      | Integer         | Memory allocated to Yarn. The unit is MB.                                                                    |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNMemoryAvailable                      | Integer         | Available memory on Yarn. The unit is MB.                                                                    |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNMemoryAvailablePercentage            | Percentage      | Percentage of available memory on Yarn, that is, the proportion of available memory to total memory on Yarn  |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 100                                                                                        |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                 | YARNMemoryPending                        | Integer         | Pending memory on Yarn                                                                                       |
   |                 |                                          |                 |                                                                                                              |
   |                 |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-----------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+

.. note::

   -  When the value type is percentage or ratio in :ref:`Table 1 <mrs_01_0061__table15133845184415>`, the valid value can be accurate to percentile. The percentage metric value is a decimal value with a percent sign (%) removed. For example, 16.80 represents 16.80%.
   -  Hybrid clusters support all metrics of analysis and streaming clusters.

   When the value type is percentage or ratio in :ref:`Table 2 <mrs_01_0061__table12336184610200>`, the valid value can be accurate to percentile. The percentage metric value is a decimal value with a percent sign (%) removed. For example, 16.80 represents 16.80%.

When adding a resource plan, you can set parameters by referring to :ref:`Table 3 <mrs_01_0061__table1846575414619>`.

.. _mrs_01_0061__table1846575414619:

.. table:: **Table 3** Configuration items of a resource plan

   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuration Item | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   +====================+=====================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Time Range         | Start time and End time of a resource plan are accurate to minutes, with the value ranging from **00:00** to **23:59**. For example, if a resource plan starts at 8:00 and ends at 10:00, set this parameter to 8:00-10:00. The end time must be at least 30 minutes later than the start time.                                                                                                                                                                                                                                                                                                     |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Node Range         | The number of nodes in a resource plan ranges from **0** to **500**. In the time range specified in the resource plan, if the number of Task nodes is less than the specified minimum number of nodes, it will be increased to the specified minimum value of the node range at a time. If the number of Task nodes is greater than the maximum number of nodes specified in the resource plan, the auto scaling function reduces the number of Task nodes to the maximum value of the node range at a time. The minimum number of nodes must be less than or equal to the maximum number of nodes. |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  When a resource plan is enabled, the **Default Range** value on the auto scaling page forcibly takes effect beyond the time range specified in the resource plan. For example, if **Default Range** is set to **1-2**, **Time Range** is between **08:00-10:00**, and **Node Range** is **4-5** in a resource plan, the number of Task nodes in other periods (0:00-8:00 and 10:00-23:59) of a day is forcibly limited to the default node range (1 to 2). If the number of nodes is greater than 2, auto scale-in is triggered; if the number of nodes is less than 1, auto scale-out is triggered.
   -  When a resource plan is not enabled, the **Default Range** takes effect in all time ranges. If the number of nodes is not within the default node range, the number of Task nodes is automatically increased or decreased to the default node range.
   -  Time ranges of resource plans cannot be overlapped. The overlapped time range indicates that two effective resource plans exist at a time point. For example, if resource plan 1 takes effect from **08:00** to **10:00** and resource plan 2 takes effect from **09:00** to **11:00**, the time range between **09:00** to **10:00** is overlapped.
   -  The time range of a resource plan must be on the same day. For example, if you want to configure a resource plan from **23:00** to **01:00** in the next day, configure two resource plans whose time ranges are **23:00-00:00** and **00:00-01:00**, respectively.

When adding an automation script, you can set related parameters by referring to :ref:`Table 4 <mrs_01_0061__table15644113520578>`.

.. _mrs_01_0061__table15644113520578:

.. table:: **Table 4** Configuration items of an automation script

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuration Item                | Description                                                                                                                                                                                               |
   +===================================+===========================================================================================================================================================================================================+
   | Name                              | Automation script name.                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                           |
   |                                   | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and must not start with a space.                                                                                     |
   |                                   |                                                                                                                                                                                                           |
   |                                   | The value can contain 1 to 64 characters.                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    A name must be unique in the same cluster. You can set the same name for different clusters.                                                                                                           |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Script Path                       | Script path. The value can be an OBS file system path or a local VM path.                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   | -  An OBS file system path must start with **s3a://** and end with **.sh**, for example, **s3a://mrs-samples/**\ *xxx*\ **.sh**.                                                                          |
   |                                   | -  A local VM path must start with a slash (/) and end with **.sh**. For example, the path of the example script for installing the Zepelin is **/opt/bootstrap/zepelin/zepelin_install.sh**.             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Execution Node                    | Select a type of the node where an automation script is executed.                                                                                                                                         |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    -  If you select **Master** nodes, you can choose whether to run the script only on the active Master nodes by enabling or disabling the **Active Master** switch.                                     |
   |                                   |    -  If you enable it, the script runs only on the active Master nodes. If you disable it, the script runs on all Master nodes. This switch is disabled by default.                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Automation script parameter. The following predefined variables can be imported to obtain auto scaling information:                                                                                       |
   |                                   |                                                                                                                                                                                                           |
   |                                   | -  **${mrs_scale_node_num}**: Number of auto scaling nodes. The value is always positive.                                                                                                                 |
   |                                   | -  **${mrs_scale_type}**: Scale-out/in type. The value can be **scale_out** or **scale_in**.                                                                                                              |
   |                                   | -  **${mrs_scale_node_hostnames}**: Host names of the auto scaling nodes. Use commas (,) to separate multiple host names.                                                                                 |
   |                                   | -  **${mrs_scale_node_ips}**: IP address of the auto scaling nodes. Use commas (,) to separate multiple IP addresses.                                                                                     |
   |                                   | -  **${mrs_scale_rule_name}**: Name of the triggered auto scaling rule. For a resource plan, this parameter is set to **resource_plan**.                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Executed                          | Time for executing an automation script. The following four options are supported: **Before scale-out**, **After scale-out**, **Before scale-in**, and **After scale-in**.                                |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    Assume that the execution nodes include Task nodes.                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    -  The automation script executed before scale-out cannot run on the Task nodes to be added.                                                                                                           |
   |                                   |    -  The automation script executed after scale-out can run on the added Task nodes.                                                                                                                     |
   |                                   |    -  The automation script executed before scale-in can run on Task nodes to be deleted.                                                                                                                 |
   |                                   |    -  The automation script executed after scale-in cannot run on the deleted Task nodes.                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Action upon Failure               | Whether to continue to execute subsequent scripts and scale-out/in after the script fails to be executed.                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    -  You are advised to set this parameter to **Continue** in the commissioning phase so that the cluster can continue the scale-out/in operation no matter whether the script is executed successfully. |
   |                                   |    -  If the script fails to be executed, view the log in **/var/log/Bootstrap** on the cluster VM.                                                                                                       |
   |                                   |    -  The scale-in operation cannot be rolled back. Therefore, the **Action upon Failure** can only be set to **Continue** after scale-in.                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   The automation script is triggered only during auto scaling. It is not triggered when the cluster node is manually scaled out or in.
