:original_name: admin_guide_000111.html

.. _admin_guide_000111:

Deleting a Resource Pool
========================

Scenario
--------

If a resource pool is no longer used based on service requirements, you can delete it on FusionInsight Manager.

Prerequisites
-------------

-  Any queue in the cluster does not use the resource pool to be deleted as the default resource pool. Before deleting the resource pool, cancel the default resource pool. For details, see :ref:`Configuring a Queue <admin_guide_000112>`.
-  Resource distribution policies of all queues have been cleared from the resource pool to be deleted. For details, see :ref:`Clearing Queue Configurations <admin_guide_000114>`.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **Tenant Resources** > **Resource Pool**.
#. Locate the row that contains the specified resource pool, and click **Delete** in the **Operation** column.
#. In the displayed dialog box, click **OK**.
