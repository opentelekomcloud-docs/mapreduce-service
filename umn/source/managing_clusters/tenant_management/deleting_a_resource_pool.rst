:original_name: mrs_01_0312.html

.. _mrs_01_0312:

Deleting a Resource Pool
========================

Scenario
--------

You can delete an existing resource pool on MRS.

Prerequisites
-------------

-  Any queue in a cluster cannot use the resource pool to be deleted as the default resource pool. Before deleting the resource pool, cancel the default resource pool. For details, see :ref:`Configuring a Queue <mrs_01_0313>`.
-  Resource distribution policies of all queues have been cleared from the resource pool being deleted. For details, see :ref:`Clearing Configuration of a Queue <mrs_01_0315>`.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenant**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Deleting a Resource Pool <mrs_01_0546>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. Click the **Resource Pools** tab.

#. Locate the row that contains the specified resource pool, and click **Delete** in the **Operation** column.

   In the displayed dialog box, click **OK**.
