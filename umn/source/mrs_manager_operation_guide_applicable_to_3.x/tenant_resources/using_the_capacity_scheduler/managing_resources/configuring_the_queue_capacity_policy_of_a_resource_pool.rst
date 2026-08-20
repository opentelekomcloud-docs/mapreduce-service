:original_name: admin_guide_000131.html

.. _admin_guide_000131:

Configuring the Queue Capacity Policy of a Resource Pool
========================================================

Scenario
--------

After a resource pool is added, you can configure the capacity policy of available resources for Yarn queues so that jobs in the queues can be properly executed in the resource pool. A queue can have the queue capacity policy of only one resource pool.

You can view queues and configure queue capacity policies in any resource pool. After the queue policies are configured, Yarn queues are associated with resource pools.

Prerequisites
-------------

A queue has been added, that is, a tenant associated with computing resources has been created.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **Tenant Resources** > **Dynamic Resource Plan**.

   The **Resource Distribution Policy** page is displayed by default.

#. Select the name of the target cluster from **Cluster** and select a resource pool from **Resource Pool**.

#. Locate the row that contains the target resource name in the **Resource Allocation** area, and click **Modify** in the **Operation** column.

#. In the **Modify Resource Allocation** window, configure the resource capacity policy of the queue in the resource pool.

   -  **Capacity (%)**: indicates the percentage of computing resources used by the current tenant.
   -  **Maximum Capacity (%)**: indicates the maximum percentage of computing resources used by the current tenant.

#. On the **Modify Resource Allocation** page, click **Scheduled Policy** and set the user scheduling policy. (This operation is supported only in MRS 3.6.0 and later versions.)

   -  Click **Add Scheduled Policy** to add a scheduled policy.

      -  **Policy Name**: Enter a name of a scheduled policy, which is used to distinguish active policies in logs.

      -  **Policy Frequency**: Select **Daily**, **Weekly**, or **Monthly**.

      -  **Repeats On**: Select one or more days in a week or month for the policy to take effect. This parameter is displayed only when **Policy Frequency** is set to **Weekly** or **Monthly**.

      -  **Time Window**: Select the time range in which the policy takes effect on the specified days. You can add multiple time ranges. The time range must be at least 2 hours.

         For example, if this parameter is set to 08:00-16:00, the policy takes effect only in this time range.

      -  **Resource Capacity(%)**: Resource capacity when the policy takes effect.

      -  **Maximum Resource Capacity(%)**: Maximum resource capacity when the policy takes effect.

      -  **Enable Policy**: Determine whether the policy takes effect within the specified time. Only one policy is allowed for a queue at a time.

      .. important::

         -  The resource configuration of queues and their sibling queues in a scheduled policy supports only the percentage-based allocation and does not support the absolute values.
         -  If a scheduled policy that is taking effect is deleted, the default configuration is restored within ten minutes.
         -  The scheduled policy is checked periodically. The check period is controlled by the parameter **yarn.resourcemanager.time-policy.check-interval-secs**. To change the parameter value, log in to Manager, choose **Cluster** > **Services** > **Yarn** > **Configurations** > **All Configurations**. Search for the parameter and change its value. Then restart the instance for the change to take effect.
         -  A maximum of three scheduled policies can be added, and only one policy is allowed for each policy frequency.
         -  Only one scheduled policy can be valid at a time.
         -  After a scheduled policy takes effect, the total capacity cannot exceed 100.

   -  Click **Modify** in the **Operation** column to modify an existing scheduled policy.
   -  Click **Clear** in the **Operation** column to delete an existing scheduled policy.

#. Click **OK**.

   .. note::

      After the resource capacity values of a queue are deleted and saved, the resource capacity policy of the queue in the resource pool is canceled, indicating that the queue is disassociated from the resource pool. To achieve this, you need to change the default resource pool of the queue to another one. For details, see :ref:`Configuring a Queue <admin_guide_000130>`.
