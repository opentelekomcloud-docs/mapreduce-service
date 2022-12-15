:original_name: mrs_01_0310.html

.. _mrs_01_0310:

Creating a Resource Pool
========================

Scenario
--------

In an MRS cluster, users can logically divide Yarn cluster nodes to combine multiple NodeManagers into a Yarn resource pool. Each NodeManager belongs to one resource pool only. The system contains a **default** resource pool by default. All NodeManagers that are not added to customized resource pools belong to this resource pool.

You can create a customized resource pool on MRS and add hosts that have not been added to other customized resource pools to it.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Creating a Resource Pool <mrs_01_0544>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. Click the **Resource Pools** tab.
#. Click **Create Resource Pool**.
#. In **Create Resource Pool**, set the properties of the resource pool.

   -  **Name**: Enter a name for the resource pool. The name of the newly created resource pool cannot be **default**.

      The name consists of 1 to 20 characters and can contain digits, letters, and underscores (_) but cannot start with an underscore (_).

   -  **Available Hosts**: In the host list on the left, select a specified host name and add it to the resource pool. Only hosts in the cluster can be selected. The host list of a resource pool can be left blank.

#. Click **OK**.
#. After a resource pool is created, users can view the **Name**, **Members**, **Type**, **vCore** and **Memory** in the resource pool list. Hosts that are added to the customized resource pool are no longer members of the **default** resource pool.
