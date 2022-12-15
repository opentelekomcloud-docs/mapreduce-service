:original_name: mrs_01_0309.html

.. _mrs_01_0309:

Restoring Tenant Data
=====================

Scenario
--------

Tenant data is stored on Manager and in cluster components by default. When components are restored from faults or reinstalled, some tenant configuration data may be abnormal. In this case, you can manually restore the tenant data.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Restoring Tenant Data <mrs_01_0543>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. In the tenant list on the left, click a tenant node.

#. Check the status of the tenant data.

   a. In **Summary**, check the color of the circle on the left of **Basic Information**. Green indicates that the tenant is available and gray indicates that the tenant is unavailable.
   b. Click **Resources** and check the circle on the left of **Yarn** or **HDFS Storage**. Green indicates that the resource is available, and gray indicates that the resource is unavailable.
   c. Click **Service Association** and check the **Status** column of the associated service table. **Good** indicates that the component can provide services for the associated tenant. **Bad** indicates that the component cannot provide services for the tenant.
   d. If any check result is abnormal, go to :ref:`4 <mrs_01_0309__li10849798195335>` to restore tenant data.

#. .. _mrs_01_0309__li10849798195335:

   Click **Restore Tenant Data**.

#. In the **Restore Tenant Data** window, select one or more components whose data needs to be restored. Click **OK**. The system automatically restores the tenant data.
