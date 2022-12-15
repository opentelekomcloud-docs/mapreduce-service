:original_name: mrs_01_0546.html

.. _mrs_01_0546:

Deleting a Resource Pool
========================

Scenario
--------

You can delete an existing resource pool on MRS Manager.

Prerequisites
-------------

-  Any queue in a cluster cannot use the resource pool to be deleted as the default resource pool. Before deleting the resource pool, cancel the default resource pool. For details, see :ref:`Configuring a Queue <mrs_01_0547>`.
-  Resource distribution policies of all queues have been cleared from the resource pool being deleted. For details, see :ref:`Clearing Configuration of a Queue <mrs_01_0549>`.

Procedure
---------

#. On MRS Manager, click **Tenant**.

#. Click the **Resource Pools** tab.

#. Locate the row that contains the specified resource pool, and click **Delete** in the **Operation** column.

   In the displayed dialog box, click **OK**.
