:original_name: mrs_01_0307.html

.. _mrs_01_0307:

Deleting a Tenant
=================

Scenario
--------

You can delete a tenant that is not required on MRS.

Prerequisites
-------------

-  A tenant has been added.
-  You have checked whether the tenant to be deleted has sub-tenants. If the tenant has sub-tenants, delete them; otherwise, you cannot delete the tenant.
-  The role of the tenant to be deleted cannot be associated with any user or user group. For details about how to cancel the binding between a role and a user, see :ref:`Modifying User Information <mrs_01_0346>`.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Deleting a tenant <mrs_01_0541>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. In the tenant list on the left, move the cursor to the tenant node to be deleted and click **Delete**.

   The **Delete Tenant** dialog box is displayed. If you want to save the tenant data, select **Reserve the data of this tenant**. Otherwise, the tenant's storage space will be deleted.

#. Click **OK**.

   It takes a few minutes to save the configuration. After the tenant is deleted successfully, the role and storage space of the tenant are also deleted.

   .. note::

      -  After the tenant is deleted, the task queue of the tenant still exists in Yarn.
      -  If you choose not to reserve data when deleting the parent tenant, data of sub-tenants is also deleted if the sub-tenants use storage resources.
