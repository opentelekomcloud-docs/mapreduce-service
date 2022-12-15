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

#. Log in to FusionInsight Manager.

#. Choose **Tenant Resources** > **Dynamic Resource Plan**.

   The **Resource Distribution Policy** page is displayed by default.

#. Select the name of the target cluster from **Cluster** and select a resource pool from **Resource Pool**.

#. Locate the row that contains the target resource name in the **Resource Allocation** area, and click **Modify** in the **Operation** column.

#. In the **Modify Resource Allocation** window, configure the resource capacity policy of the queue in the resource pool.

   -  **Capacity (%)**: indicates the percentage of computing resources used by the current tenant.
   -  **Maximum Capacity (%)**: indicates the maximum percentage of computing resources used by the current tenant.

#. Click **OK**.

   .. note::

      After the resource capacity values of a queue are deleted and saved, the resource capacity policy of the queue in the resource pool is canceled, indicating that the queue is disassociated from the resource pool. To achieve this, you need to change the default resource pool of the queue to another one. For details, see :ref:`Configuring a Queue <admin_guide_000130>`.
