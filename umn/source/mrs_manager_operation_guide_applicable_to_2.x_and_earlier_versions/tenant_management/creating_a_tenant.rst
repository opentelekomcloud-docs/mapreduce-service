:original_name: mrs_01_0539.html

.. _mrs_01_0539:

Creating a Tenant
=================

Scenario
--------

You can create a tenant on MRS Manager to specify the resource usage.

Prerequisites
-------------

-  A tenant name has been planned. The name must not be the same as that of a role or Yarn queue that exists in the current cluster.
-  If a tenant requires storage resources, a storage directory has been planned based on service requirements, and the planned directory does not exist under the HDFS directory.
-  The resources that can be allocated to the current tenant have been planned and the sum of the resource percentages of direct sub-tenants under the parent tenant at every level does not exceed 100%.

Procedure
---------

#. On MRS Manager, click **Tenant**.

#. Click **Create Tenant**. On the page that is displayed, configure tenant properties.

   .. table:: **Table 1** Tenant parameters

      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                    |
      +=========================================+================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | Name                                    | Specifies the name of the current tenant. The value consists of 3 to 20 characters, and can contain letters, digits, and underscores (_).                                                                                                                                                                                                                                                                                      |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tenant Type                             | The options include **Leaf** and **Non-leaf**. If **Leaf** is selected, the current tenant is a leaf tenant and no sub-tenant can be added. If **Non-leaf** is selected, sub-tenants can be added to the current tenant.                                                                                                                                                                                                       |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dynamic Resources                       | Specifies the dynamic computing resources for the current tenant. The system automatically creates a task queue named after the tenant name in Yarn. When dynamic resources are not **Yarn**, the system does not automatically create a task queue.                                                                                                                                                                           |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool Capacity (%)      | Specifies the percentage of the computing resources used by the current tenant in the **default** resource pool.                                                                                                                                                                                                                                                                                                               |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool Max. Capacity (%) | Specifies the maximum percentage of the computing resources used by the current tenant in the **default** resource pool.                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Resource                        | Specifies storage resources for the current tenant. The system automatically creates a file folder named after the tenant name in the **/tenant** directory. When a tenant is created for the first time, the system automatically creates the **/tenant** directory in the HDFS root directory. If storage resources are not **HDFS**, the system does not create a storage directory under the root directory of HDFS.       |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Space Quota (MB)                        | Specifies the quota for HDFS storage space used by the current tenant. The value ranges from **1** to **8796093022208**. The unit is MB. This parameter indicates the maximum HDFS storage space that can be used by a tenant, but does not indicate the actual space used. If the value is greater than the size of the HDFS physical disk, the maximum space available is the full space of the oHDFS physical disk.         |
      |                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                |
      |                                         | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                      |
      |                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                |
      |                                         |    To ensure data reliability, one copy of a file is automatically generated when the file is stored in HDFS. That is, two copies of the same file are stored by default. The HDFS storage space indicates the total disk space occupied by all these copies. For example, if the value of **Storage Space Quota** is set to **500**, the actual space for storing files is about 250 MB (500/2 = 250).                        |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Storage Path**                        | Specifies the tenant's HDFS storage directory. The system automatically creates a file folder named after the tenant name in the **/tenant** directory by default. For example, the default HDFS storage directory for tenant **ta1** is **tenant/ta1**. When a tenant is created for the first time, the system automatically creates the **/tenant** directory in the HDFS root directory. The storage path is customizable. |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Service                                 | Specifies other service resources associated with the current tenant. HBase is supported. To configure this parameter, click **Associate Services**. In the dialog box that is displayed, set **Service** to **HBase**. If **Association Mode** is set to **Exclusive**, service resources are occupied exclusively. If **share** is selected, service resources are shared.                                                   |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                             | Specifies the description of the current tenant.                                                                                                                                                                                                                                                                                                                                                                               |
      +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK** to save the settings.

   It takes a few minutes to save the settings. If the **Tenant created successfully** is displayed in the upper-right corner, the tenant is added successfully.

   .. note::

      -  Roles, computing resources, and storage resources are automatically created when tenants are created.
      -  The new role has permissions on the computing and storage resources. The role and its permissions are controlled by the system automatically and cannot be controlled manually under **Manage Role**.
      -  If you want to use the tenant, create a system user and assign the Manager_tenant role and the role corresponding to the tenant to the user. For details, see :ref:`Creating a User <mrs_01_0422>`.

Related Tasks
-------------

Viewing an added tenant

#. On MRS Manager, click **Tenant**.

#. In the tenant list on the left, click the name of the added tenant.

   The **Summary** tab is displayed on the right by default.

#. View **Basic Information**, **Resource Quota**, and **Statistics** of the tenant.

   If HDFS is in the **Stopped** state, **Available** and **Used** of **Space** in **Resource Quota** are **unknown.**
