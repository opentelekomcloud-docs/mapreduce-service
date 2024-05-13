:original_name: admin_guide_000119.html

.. _admin_guide_000119:

Adding a Sub-Tenant
===================

Scenario
--------

You can create sub-tenants on MRS Manager and allocate resources of the current tenant to the sub-tenants based on the resource consumption and isolation planning and requirements of services.

Prerequisites
-------------

-  A parent non-leaf tenant has been added.
-  A tenant name has been planned based on service requirements. The name cannot be the same as that of a role, HDFS directory, or Yarn queue that exists in the current cluster.
-  Resources to be allocated to the current tenant have been planned to ensure that the sum of resources of direct sub-tenants at each level does not exceed the resources of the current tenant.

Procedure
---------

#. Log in to MRS Manager and choose **Tenant Resources**.

#. In the tenant list on the left, select a parent tenant and click |image1|. On the page for adding a sub-tenant, set attributes for the sub-tenant according to :ref:`Table 1 <admin_guide_000119__tc983b52ccd084798871c7fa2b49856dd>`.

   .. _admin_guide_000119__tc983b52ccd084798871c7fa2b49856dd:

   .. table:: **Table 1** Sub-tenant parameters

      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                              | Description                                                                                                                                                                                                                                                                              |
      +========================================+==========================================================================================================================================================================================================================================================================================+
      | Cluster                                | Indicates the cluster to which the parent tenant belongs.                                                                                                                                                                                                                                |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parent Tenant Resource                 | Indicates the name of the parent tenant.                                                                                                                                                                                                                                                 |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Name                                   | -  Indicates the name of the current tenant. The value consists of 3 to 50 characters, including digits, letters, and underscores (_).                                                                                                                                                   |
      |                                        | -  Plan a sub-tenant name based on service requirements. The name cannot be the same as that of a role, HDFS directory, or Yarn queue that exists in the current cluster.                                                                                                                |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tenant Type                            | Specifies whether the tenant is a leaf tenant.                                                                                                                                                                                                                                           |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  When **Leaf Tenant** is selected, the current tenant is a leaf tenant and no sub-tenant can be added.                                                                                                                                                                                 |
      |                                        | -  When **Non-leaf Tenant** is selected, the current tenant is not a leaf tenant and sub-tenants can be added to the current tenant. However, the tenant depth cannot exceed 5 levels.                                                                                                   |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Computing Resource                     | Specifies the dynamic computing resources for the current tenant.                                                                                                                                                                                                                        |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  When **Yarn** is selected, the system automatically creates a queue in Yarn and the queue is named the same as the sub-tenant name.                                                                                                                                                   |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        |    -  A leaf tenant can directly submit jobs to the queue.                                                                                                                                                                                                                               |
      |                                        |    -  A non-leaf tenant cannot directly submit jobs to the queue. However, Yarn adds an extra queue (hidden) named **default** for the non-leaf tenant to record the remaining resource capacity of the tenant. Actual jobs do not run in this queue.                                    |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  If **Yarn** is not selected, the system does not automatically create a queue.                                                                                                                                                                                                        |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool Capacity (%)     | Indicates the percentage of computing resources used by the current tenant. The base value is the total resources of the parent tenant.                                                                                                                                                  |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool Max Capacity (%) | Indicates the maximum percentage of computing resources used by the current tenant. The base value is the total resources of the parent tenant.                                                                                                                                          |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Resource                       | Specifies storage resources for the current tenant.                                                                                                                                                                                                                                      |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  When **HDFS** is selected, the system automatically creates a folder named after the sub-tenant in the HDFS parent tenant directory.                                                                                                                                                  |
      |                                        | -  When **HDFS** is not selected, the system does not automatically allocate storage resources.                                                                                                                                                                                          |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Quota                                  | Indicates the quota for files and directories.                                                                                                                                                                                                                                           |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Space Quota                            | Indicates the quota for the HDFS storage space used by the current tenant.                                                                                                                                                                                                               |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  If the unit is set to **MB**, the value ranges from **1** to **8796093022208**. If the unit is set to **GB**, the value ranges from **1** to **8589934592**.                                                                                                                          |
      |                                        | -  This parameter indicates the maximum HDFS storage space that can be used by the tenant, but not the actual space used.                                                                                                                                                                |
      |                                        | -  If its value is greater than the size of the HDFS physical disk, the maximum space available is the full space of the HDFS physical disk.                                                                                                                                             |
      |                                        | -  If this quota is greater than the quota of the parent tenant, the actual storage space does not exceed the quota of the parent tenant.                                                                                                                                                |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Path                           | Indicates the HDFS storage directory for the tenant.                                                                                                                                                                                                                                     |
      |                                        |                                                                                                                                                                                                                                                                                          |
      |                                        | -  The system automatically creates a folder named after the sub-tenant name in the directory of the parent tenant by default. For example, if the sub-tenant is **ta1s** and the parent directory is **/tenant/ta1**, the storage path for the sub-tenant is then **/tenant/ta1/ta1s**. |
      |                                        | -  The storage path is customizable in the parent directory.                                                                                                                                                                                                                             |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                            | Indicates the description of the current tenant.                                                                                                                                                                                                                                         |
      +----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      Roles, computing resources, and storage resources are automatically created when tenants are created.

      -  The new role has permissions on the computing and storage resources. This role and its permissions are automatically controlled by the system and cannot be manually managed by choosing **System** > **Permission** > **Role**. The role name is in the format of *Tenant name*\ \_\ *Cluster ID*. The ID of the first cluster is not displayed by default.
      -  When using this tenant, create a system user and bind the user to the role of the tenant. For details, see :ref:`Adding a User and Binding the User to a Tenant Role <admin_guide_000120>`.
      -  The sub-tenant can further allocate the resources of its parent tenant. The sum of the resource percentages of direct sub-tenants under a parent tenant at each level cannot exceed 100%. The sum of the computing resource percentages of all level-1 tenants cannot exceed 100%.

#. Check whether the current tenant needs to be associated with resources of other services.

   -  If yes, go to :ref:`4 <admin_guide_000119__lcdfcd36b99d84c3ba2f290f976ade15b>`.
   -  If no, go to :ref:`5 <admin_guide_000119__l93b6a287f2a9444f9b34fcbcc1e595ac>`.

#. .. _admin_guide_000119__lcdfcd36b99d84c3ba2f290f976ade15b:

   Click **Associate Service** to configure other service resources used by the current tenant.

   a. Set **Services** to **HBase**.
   b. Set **Association Type** as follows:

      -  **Exclusive** indicates that the service resources are used by the tenant exclusively and cannot be associated with other tenants.
      -  **Shared** indicates that the service resources can be shared with other tenants.

   .. note::

      -  Only HBase can be associated with a new tenant. However, HDFS, HBase, and Yarn can be associated with existing tenants.
      -  To associate an existing tenant with service resources, click the target tenant in the tenant list, switch to the **Service Associations** page, and click **Associate Service** to configure resources to be associated with the tenant.
      -  To disassociate an existing tenant from service resources, click the target tenant in the tenant list, switch to the **Service Associations** page, and click **Delete** in the **Operation** column. In the displayed dialog box, select **I have read the information and understand the impact** and click **OK**.

   c. Click **OK**.

#. .. _admin_guide_000119__l93b6a287f2a9444f9b34fcbcc1e595ac:

   Click **OK**. Wait until the system displays a message indicating that the tenant is successfully created.

.. |image1| image:: /_static/images/en-us_image_0000001442653665.png
