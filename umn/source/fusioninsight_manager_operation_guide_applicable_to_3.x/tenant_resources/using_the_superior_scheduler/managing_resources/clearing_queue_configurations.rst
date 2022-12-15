:original_name: admin_guide_000114.html

.. _admin_guide_000114:

Clearing Queue Configurations
=============================

Scenario
--------

You can clear the configurations of a queue on FusionInsight MRS Manager when the queue does not need resources of a resource pool or the resource pool needs to be disassociated from the queue. Clearing queue configurations cancels the resource capacity policy of the queue in the resource pool.

Prerequisites
-------------

You have changed the default resource pool of the queue to another one. If a queue is to be disassociated from a resource pool, this resource pool cannot serve as the default resource pool of the queue. For details, see :ref:`Configuring a Queue <admin_guide_000112>`.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **Tenant Resources** > **Dynamic Resource Plan**.
#. Select the name of the target cluster from **Cluster** and select a resource pool from **Resource Pool**.
#. Locate the row that contains the target resource name in the **Resource Allocation** area, and click **Clear** in the **Operation** column.
#. In the displayed dialog box, click **OK** to clear the queue configurations from the current resource pool.
