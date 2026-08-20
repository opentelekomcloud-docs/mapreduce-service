:original_name: admin_guide_000113.html

.. _admin_guide_000113:

Configuring the Queue Capacity Policy of a Resource Pool
========================================================

Scenario
--------

After a resource pool is added, you can configure the capacity policy of available resources for Yarn queues so that jobs in the queues can be properly executed in the resource pool.

This section describes how to configure the queue policy on MRS Manager. Tenant queues equipped with the Superior scheduler can use resources in different resource pools.

Prerequisites
-------------

-  You have logged in to MRS Manager.

-  A resource pool has been added.
-  The target queue is not associated with the resource pools of other queues except the default resource pool.

Procedure
---------

#. On MRS Manager, choose **Tenant Resources**.
#. Choose **Dynamic Resource Plan**.
#. Click the **Resource Distribution Policy** tab.
#. Select the name of the target cluster from **Cluster** and select a resource pool from **Resource Pool**.
#. Locate the row that contains the target queue in the **Resource Allocation** area, and click **Modify** in the **Operation** column.
#. On the **Resource Configuration Policy** tab of the **Modify Resource Allocation** window, set the resource configuration policy of the queue in the resource pool.

   -  **Weight**: indicates the resources that a tenant can obtain. Its initial value is the same as the minimum resource percentage.
   -  **Minimum Resource**: indicates the minimum resources that a tenant can obtain.
   -  **Maximum Resource**: indicates the maximum resources that a tenant can obtain.
   -  **Reserved Resource**: indicates the resources that are reserved for the tenant's queues and cannot be lent to other tenants' queues.

#. Click the **User Policy** tab in the **Modify Resource Allocation** window and set the user policy.

   .. note::

      **defaultUser(built-in)** indicates that the policy specified for **defaultUser** is used if a user does not have a policy. The default policy cannot be deleted.

   -  Click **Add User Policy** to add a user policy.

      -  **Username**: indicates the name of a user.
      -  **Priority**: When task queues need to compete for resources, a queue with a higher priority obtains resources first. However, not all containers can be started. (This parameter is displayed for MRS 3.5.0 and later versions only.)
      -  **Max vCores**: indicates the maximum number of virtual cores that the user can obtain.
      -  **Max Memory(MB)**: indicates the maximum memory that the user can obtain.

   -  Click **Modify** in the **Operation** column to modify an existing user policy.
   -  Click **Clear** in the **Operation** column to delete an existing user policy.

#. Go to the **Modify Resource Allocation** page, click the **Scheduled Policy** tab, and set the user scheduling policy. (This operation is supported only in MRS 3.6.0 and later versions.)

   -  Click **Add Scheduled Policy** to add a scheduled policy.

      -  **Policy Name**: Enter a name of a scheduled policy, which is used to distinguish active policies in logs.

      -  **Policy Frequency**: Select **Daily**, **Weekly**, or **Monthly**.

      -  **Repeats On**: Select one or more days in a week or month for the policy to take effect. This parameter is displayed only when **Policy Frequency** is set to **Weekly** or **Monthly**.

      -  **Time Window**: Select the time range in which the policy takes effect on the specified days. You can add multiple time ranges. The time range must be at least 2 hours.

         For example, if this parameter is set to 08:00-16:00, the policy takes effect only in this time range.

      -  **Weight**: Set the weight of a queue when the policy takes effect.

      -  **Minimum Resource**: Set the minimum resources allocated to a queue when the policy takes effect.

      -  **Maximum Resource**: Set the maximum resources allocated to a queue when the policy takes effect.

      -  **Reserved Resource**: Set the resources reserved for a queue when the policy takes effect.

      -  **Enable Policy**: Determine whether the policy takes effect within the specified time. Only one policy is allowed for a queue at a time.

      .. important::

         -  The resource configuration of queues and their sibling queues in a scheduled policy supports only the percentage-based allocation and does not support the absolute values.
         -  If a scheduled policy that is taking effect is deleted, the default configuration is restored within ten minutes.
         -  The scheduled policy is checked periodically. The check period is controlled by the parameter **yarn.resourcemanager.time-policy.check-interval-secs**. To change the parameter value, log in to Manager, choose **Cluster** > **Services** > **Yarn** > **Configurations** > **All Configurations**. Search for the parameter and change its value. Then restart the instance for the change to take effect.
         -  A maximum of three scheduled policies can be added, and only one policy is allowed for each policy frequency.
         -  Only one scheduled policy can be valid at a time.
         -  The sum of minimum and maximum resources in a scheduled policy cannot exceed 100 after the policy takes effect.

   -  Click **Modify** in the **Operation** column to modify an existing scheduled policy.
   -  Click **Clear** in the **Operation** column to delete an existing scheduled policy.

#. Click **OK**.
