:original_name: admin_guide_000113.html

.. _admin_guide_000113:

Configuring the Queue Capacity Policy of a Resource Pool
========================================================

Scenario
--------

After a resource pool is added, you can configure the capacity policy of available resources for Yarn queues so that jobs in the queues can be properly executed in the resource pool.

This section describes how to configure the queue policy on FusionInsight Manager. Tenant queues equipped with the Superior scheduler can use resources in different resource pools.

Prerequisites
-------------

-  You have logged in to FusionInsight Manager.

-  A resource pool has been added.
-  The target queue is not associated with the resource pools of other queues except the default resource pool.

Procedure
---------

#. On FusionInsight Manager, choose **Tenant Resources**.
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
      -  **Weight**: indicates the resources that the user can obtain.
      -  **Max vCores**: indicates the maximum number of virtual cores that the user can obtain.
      -  **Max Memory(MB)**: indicates the maximum memory that the user can obtain.

   -  Click **Modify** in the **Operation** column to modify an existing user policy.
   -  Click **Clear** in the **Operation** column to delete an existing user policy.

#. Click **OK**.
