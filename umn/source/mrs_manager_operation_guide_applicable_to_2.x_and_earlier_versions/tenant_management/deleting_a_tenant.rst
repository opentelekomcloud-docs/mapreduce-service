:original_name: mrs_01_0541.html

.. _mrs_01_0541:

Deleting a tenant
=================

Scenario
--------

You can delete a tenant that is not required on MRS Manager.

Prerequisites
-------------

-  A tenant has been added.
-  You have checked whether the tenant to be deleted has sub-tenants. If the tenant has sub-tenants, delete them; otherwise, you cannot delete the tenant.
-  The role of the tenant to be deleted cannot be associated with any user or user group. For details about how to cancel the binding between a role and a user, see :ref:`Modifying User Information <mrs_01_0423>`.

Procedure
---------

#. On MRS Manager, click **Tenant**.

#. In the tenant list on the left, move the cursor to the tenant node to be deleted and click **Delete**.

   The **Delete Tenant** dialog box is displayed. If you want to save the tenant data, select **Reserve the data of this tenant**. Otherwise, the tenant's storage space will be deleted.

#. Click OK to save the settings.

   It takes a few minutes to save the configuration. After the tenant is deleted successfully, the role and storage space of the tenant are also deleted.

   .. note::

      -  After the tenant is deleted, the task queue of the tenant still exists in Yarn.
      -  If you choose not to reserve data when deleting the parent tenant, data of sub-tenants is also deleted if the sub-tenants use storage resources.
