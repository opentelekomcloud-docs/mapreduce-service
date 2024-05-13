:original_name: admin_guide_000092.html

.. _admin_guide_000092:

Multi-Tenant Model
==================

Related Model
-------------

The following figure shows a multi-tenant model.

.. _admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0:

.. figure:: /_static/images/en-us_image_0000001392733950.png
   :alt: **Figure 1** Multi-tenant model

   **Figure 1** Multi-tenant model

:ref:`Table 1 <admin_guide_000092__t8493e085f6bc470eb314c82866f86756>` describes the concepts involved in :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`.

.. _admin_guide_000092__t8493e085f6bc470eb314c82866f86756:

.. table:: **Table 1** Concepts in the model

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Concept                           | Description                                                                                                                                                                                                                                                                          |
   +===================================+======================================================================================================================================================================================================================================================================================+
   | User                              | A natural person who has a username and password and uses the big data cluster.                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | There are three different users in :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`: user A, user B, and user C.                                                                                                                                              |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Role                              | A role is a carrier of one or more permissions. Permissions are assigned to specific objects, for example, access permissions for the **/tenant** directory in HDFS.                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>` shows four roles: **t1**, **t2**, **t3**, and **Manager_tenant**.                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | -  Roles **t1**, **t2**, and **t3** are automatically generated when tenants are created. The role names are the same as the tenant names. That is, roles **t1**, **t2**, and **t3** map to tenants **t1**, **t2**, and **t3**. Role names and tenant names need to be used in pair. |
   |                                   | -  Role **Manager_tenant** is defaulted in the cluster and cannot be used separately.                                                                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tenant                            | A tenant is a resource set in a big data cluster. Multiple tenants are referred to as multi-tenancy. The resource sets further divided under a tenant are called sub-tenants.                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>` shows three tenants: **t1**, **t2**, and **t3**.                                                                                                                                                             |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource                          | -  Computing resources include CPUs and memory.                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   |    The computing resources of a tenant are allocated from the total computing resources in the cluster. One tenant cannot occupy the computing resources of another tenant.                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   |    In :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`, computing resources 1, 2, and 3 are allocated for tenants **t1**, **t2**, and **t3** respectively from the cluster's computing resources.                                                             |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | -  Storage resources include disks and third-party storage systems.                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   |    The storage resources of a tenant are allocated from the total storage resources in the cluster. One tenant cannot occupy the storage resources of another tenant.                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   |    In :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`, storage resources 1, 2, and 3 are allocated for tenants **t1**, **t2**, and **t3** respectively from the cluster's storage resources.                                                                 |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

If a user wants to use a tenant's resources or add or delete a sub-tenant of a tenant, the user needs to be bound to both the tenant role and role **Manager_tenant**. :ref:`Table 2 <admin_guide_000092__tc4dc7a31593b48ab9ea2b09ea1bfc64d>` lists the roles bound to each user in :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`.

.. _admin_guide_000092__tc4dc7a31593b48ab9ea2b09ea1bfc64d:

.. table:: **Table 2** Roles bound to each user

   +-----------------------+----------------------------+--------------------------------------------------------------+
   | User                  | Role                       | Permission                                                   |
   +=======================+============================+==============================================================+
   | User A                | -  Role **t1**             | -  Uses the resources of tenants **t1** and **t2**.          |
   |                       | -  Role **t2**             | -  Adds or deletes sub-tenants of tenants **t1** and **t2**. |
   |                       | -  Role **Manager_tenant** |                                                              |
   +-----------------------+----------------------------+--------------------------------------------------------------+
   | User B                | -  Role **t3**             | -  Uses the resources of tenant **t3**.                      |
   |                       | -  Role **Manager_tenant** | -  Adds or deletes sub-tenants of tenant **t3**.             |
   +-----------------------+----------------------------+--------------------------------------------------------------+
   | User C                | -  Role **t1**             | -  Uses the resources of tenant **t1**.                      |
   |                       | -  Role **Manager_tenant** | -  Adds or deletes sub-tenants of tenant **t1**.             |
   +-----------------------+----------------------------+--------------------------------------------------------------+

A user can be bound to multiple roles, and one role can also be bound to multiple users. Users are associated with tenants after being bound to the tenant roles. Therefore, tenants and users form a many-to-many relationship. One user can use the resources of multiple tenants, and multiple users can use the resources of the same tenant. For example, in :ref:`Figure 1 <admin_guide_000092__f486ae0dbdc8a4d6285e9d6e8ac5cbde0>`, user A uses the resources of tenants **t1** and **t2**, and users A and C uses the resources of tenant **t1**.

.. note::

   The concepts of a parent tenant, sub-tenant, level-1 tenant, and level-2 tenant are all designed for the multi-tenant service scenarios. Pay attention to the differences these concepts and the concepts of a leaf tenant resource and non-leaf tenant resource on MRS Manager.

   -  Level-1 tenant: determined based on the tenant's level. For example, the first created tenant is a level-1 tenant and its sub-tenant is a level-2 tenant.
   -  Parent tenant and sub-tenant: indicates the hierarchical relationship between tenants.
   -  Non-leaf tenant resource: indicates the tenant type selected during tenant creation. This tenant type can be used to create sub-tenants.
   -  Leaf tenant resource: indicates the tenant type selected during tenant creation. This tenant type cannot be used to create sub-tenants.

Multi-Tenant Platform
---------------------

Tenant is a core concept of the MRS big data platform. It plays an important role in big data platforms' transformation from user-centered to multi-tenant to keep up with enterprises' multi-tenant application environments. :ref:`Figure 2 <admin_guide_000092__f0b6aaf15c16f487fa23a1a04eb45754f>` shows the transformation of big data platforms.

.. _admin_guide_000092__f0b6aaf15c16f487fa23a1a04eb45754f:

.. figure:: /_static/images/en-us_image_0000001442773629.png
   :alt: **Figure 2** Platform transformation from user-centered to multi-tenant

   **Figure 2** Platform transformation from user-centered to multi-tenant

On a user-centered big data platform, users can directly access and use all resources and services.

-  However, user applications may use only partial cluster resources, resulting in low resource utilization.
-  The data of different users may be stored together, decreasing data security.

On a multi-tenant big data platform, users use required resources and services by accessing the tenants.

-  Resources are allocated and scheduled based on application requirements and used based on tenants, increasing resource utilization.
-  Users can access the resources of tenants only after being associated with tenant roles, enhancing access security.
-  The data of tenants is isolated, ensuring data security.
