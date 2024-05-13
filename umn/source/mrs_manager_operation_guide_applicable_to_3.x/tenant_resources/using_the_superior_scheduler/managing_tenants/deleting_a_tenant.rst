:original_name: admin_guide_000107.html

.. _admin_guide_000107:

Deleting a Tenant
=================

Scenario
--------

You can delete tenants that are no longer used on MRS Manager based on service requirements to release resources occupied by the tenants.

Prerequisites
-------------

-  A tenant has been added.
-  The tenant has no sub-tenants. If the tenant has sub-tenants, delete them; otherwise, the tenant cannot be deleted.
-  The role of the tenant is not associated with any user or user group.

Procedure
---------

#. Log in to MRS Manager and choose **Tenant Resources**.

#. In the tenant list on the left, click the target tenant and click |image1|.

   .. note::

      -  If you want to retain the tenant data, select **Reserve the data of this tenant resource**. Otherwise, the storage space of the tenant will be deleted.

#. Click **OK**.

   It takes a few minutes to save the configuration. After the tenant is deleted, the role and storage space of the tenant are also deleted.

   .. note::

      After the tenant is deleted, the queue of the tenant still exists in Yarn. The queue of the tenant is not displayed on the role management page in Yarn.

.. |image1| image:: /_static/images/en-us_image_0000001392414394.png
