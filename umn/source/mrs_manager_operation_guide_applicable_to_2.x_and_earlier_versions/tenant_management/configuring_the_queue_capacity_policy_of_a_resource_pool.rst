:original_name: mrs_01_0548.html

.. _mrs_01_0548:

Configuring the Queue Capacity Policy of a Resource Pool
========================================================

Scenario
--------

After a resource pool is added, the capacity policies of available resources need to be configured for Yarn task queues. This ensures that tasks in the resource pool are running properly. Each queue can be configured with the queue capacity policy of only one resource pool. Users can view the queues in any resource pool and configure queue capacity policies. After the queue policies are configured, Yarn task queues and resource pools are associated.

You can configure queue policies on MRS Manager.

Prerequisites
-------------

-  A resource pool has been added.
-  The task queues are not associated with other resource pools. By default, all queues are associated with the **Default** resource pool.

Procedure
---------

#. On MRS Manager, click **Tenant**.

#. Click the **Dynamic Resource Plan** tab.

#. In **Resource Pools**, select a specified resource pool.

   **Available Resource Quota**: indicates that all resources in each resource pool are available for queues by default.

#. Locate the specified queue in the **Resource Allocation** table, and click **Modify** in the **Operation** column.

#. In **Modify Resource Allocation**, configure the resource capacity policy of the task queue in the resource pool.

   -  **Capacity (%)**: specifies the percentage of the current tenant's computing resource usage.
   -  **Maximum Capacity (%)**: specifies the percentage of the current tenant's maximum computing resource usage.

#. Click **OK** to save the settings.
