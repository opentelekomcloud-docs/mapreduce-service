:original_name: mrs_01_0315.html

.. _mrs_01_0315:

Clearing Configuration of a Queue
=================================

Scenario
--------

Users can clear the configuration of a queue on MRS Manager when the queue does not need resources from a resource pool or if a resource pool needs to be disassociated from the queue. Clearing queue configurations means that the resource capacity policy of the queue is canceled.

Prerequisites
-------------

-  If a queue is to be unbound from a resource pool, this resource pool cannot serve as the default resource pool of the queue. Therefore, you must first change the default resource pool of the queue to another one. For details, see :ref:`Configuring a Queue <mrs_01_0313>`.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Clearing Configuration of a Queue <mrs_01_0549>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. Click the **Resource Distribution Policies** tab.

#. In **Resource Pools**, select a specified resource pool.

#. Locate the specified queue in the **Resource Allocation** table, and click **Clear** in the **Operation** column

   In the **Clear Queue Configuration** dialog box, click **OK** to clear the queue configuration in the current resource pool.

   .. note::

      If no resource capacity policy is configured for a queue, the clearing function is unavailable for the queue by default.
