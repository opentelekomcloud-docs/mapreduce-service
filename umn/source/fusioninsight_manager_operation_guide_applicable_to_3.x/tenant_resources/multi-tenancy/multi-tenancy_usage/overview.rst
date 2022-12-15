:original_name: admin_guide_000097.html

.. _admin_guide_000097:

Overview
========

Tenants are used in resource control and service isolation scenarios. Administrators need to determine the service scenarios of cluster resources and then plan tenants.

.. note::

   -  Yarn in a new cluster uses the Superior scheduler by default. For details, see :ref:`Using the Superior Scheduler <admin_guide_000099>`.

Multi-tenancy involves three types of operations: creating a tenant, managing tenants, and managing resources. :ref:`Table 1 <admin_guide_000097__tfa862b93a42b4565924842697866fde8>` describes these operations.

.. _admin_guide_000097__tfa862b93a42b4565924842697866fde8:

.. table:: **Table 1** Multi-tenant operations

   +-----------------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation             | Action                                                      | Description                                                                                                                                                                                                                                 |
   +=======================+=============================================================+=============================================================================================================================================================================================================================================+
   | Creating a tenant     | -  Add a tenant.                                            | During the creation of a tenant, you can configure its computing resources, storage resources, and associated services based on service requirements. In addition, you can add users to the tenant and bind necessary roles to these users. |
   |                       | -  Add a sub-tenant.                                        |                                                                                                                                                                                                                                             |
   |                       | -  Create a user and bind the user to the role of a tenant. | A user to create a level-1 tenant needs to be bound to the **Manager_administrator** or **System_administrator** role.                                                                                                                      |
   |                       |                                                             |                                                                                                                                                                                                                                             |
   |                       |                                                             | A user to create a sub-tenant needs to be bound to the role of the parent tenant at least.                                                                                                                                                  |
   +-----------------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Managing tenants      | -  Manage the tenant directory.                             | You can edit tenants as services change.                                                                                                                                                                                                    |
   |                       | -  Restore tenant data.                                     |                                                                                                                                                                                                                                             |
   |                       | -  Clear non-associated queues of a tenant.                 | A user to manage or delete a level-1 tenant or restore tenant data needs to be bound to the **Manager_administrator** or **System_administrator** role.                                                                                     |
   |                       | -  Delete a tenant.                                         |                                                                                                                                                                                                                                             |
   |                       |                                                             | A user to manage or delete a sub-tenant needs to be bound to the role of the parent tenant at least.                                                                                                                                        |
   +-----------------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Managing resources    | -  Create a resource pool.                                  | You can reconfigure resources for tenants as the services change.                                                                                                                                                                           |
   |                       | -  Modify a resource pool.                                  |                                                                                                                                                                                                                                             |
   |                       | -  Delete a resource pool.                                  | A user to manage resources needs to be bound to the **Manager_administrator** or **System_administrator** role.                                                                                                                             |
   |                       | -  Configure a queue.                                       |                                                                                                                                                                                                                                             |
   |                       | -  Configure the queue capacity policy of a resource pool.  |                                                                                                                                                                                                                                             |
   |                       | -  Clear configurations of a queue.                         |                                                                                                                                                                                                                                             |
   +-----------------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
