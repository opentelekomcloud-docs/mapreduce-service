:original_name: admin_guide_000098.html

.. _admin_guide_000098:

Process Overview
================

Administrators need to determine the service scenarios of cluster resources and then plan tenants. After that, administrators add tenants and configure dynamic resources, storage resources, and associated services for the tenants on FusionInsight Manager.

:ref:`Process Overview <admin_guide_000098>` shows the process for creating a tenant.


.. figure:: /_static/images/en-us_image_0000001442653645.png
   :alt: **Figure 1** Creating a tenant

   **Figure 1** Creating a tenant

:ref:`Table 1 <admin_guide_000098__t986256797c9741f79fb27fed0559d8cb>` describes the operations for creating a tenant.

.. _admin_guide_000098__t986256797c9741f79fb27fed0559d8cb:

.. table:: **Table 1** Operations for creating a tenant

   +--------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                                        | Description                                                                                                                                                                                           |
   +==================================================+=======================================================================================================================================================================================================+
   | Add a tenant.                                    | You can configure the computing resources, storage resources, and associated services of the tenant.                                                                                                  |
   +--------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Add a sub-tenant.                                | You can configure the computing resources, storage resources, and associated services of the sub-tenant.                                                                                              |
   +--------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Add a user and bind the user to the tenant role. | If a user wants to use the resources of tenant **tenant1** or add or delete sub-tenants for **tenant1**, the user must be bound to both the **Manager_tenant** and **tenant1\_**\ *Cluster ID* roles. |
   +--------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
