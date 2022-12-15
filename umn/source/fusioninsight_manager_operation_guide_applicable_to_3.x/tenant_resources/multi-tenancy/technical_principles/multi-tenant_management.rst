:original_name: admin_guide_000091.html

.. _admin_guide_000091:

Multi-Tenant Management
=======================

Unified Multi-Tenant Management
-------------------------------

Log in to FusionInsight Manager and choose **Tenant Resources** > **Tenant Resources Management**. On the page that is displayed, you can find that FusionInsight Manager is a unified multi-tenant management platform that integrates multiple functions such as tenant lifecycle management, tenant resource configuration, tenant service association, and tenant resource usage statistics, delivering a mature multi-tenant management model and achieving centralized tenant and service management.

**Graphical User Interface**

FusionInsight Manager provides the graphical multi-tenant management interface and manages and operates multiple levels of tenants using the tree structure. Additionally, FusionInsight Manager integrates the basic information and resource quota of the current tenant in one interface to facilitate O&M and management, as shown in :ref:`Figure 1 <admin_guide_000091__fig2773161717323>`.

.. _admin_guide_000091__fig2773161717323:

.. figure:: /_static/images/en-us_image_0000001369960209.png
   :alt: **Figure 1** Tenant management page of FusionInsight Manager

   **Figure 1** Tenant management page of FusionInsight Manager

**Hierarchical Tenant Management**

FusionInsight Manager supports a hierarchical tenant management model in which you can add sub-tenants to an existing tenant to re-configure resources. Sub-tenants of level-1 tenants are level-2 tenants. So on and so forth. FusionInsight Manager provides enterprises with a field-tested multi-tenant management model, enabling centralized tenant and service management.

Simplified Permission Management
--------------------------------

FusionInsight Manager hides internal permission management details from common users and simplifies permission management operations for administrators, improving usability and user experience of tenant permission management.

-  FusionInsight Manager employs role-based access control (RBAC) to configure different permissions for users based on service scenarios during multi-tenant management.
-  The administrator of tenants has tenant management permissions, including viewing resources and services of the current tenant, adding or deleting sub-tenants of the current tenant, and managing permissions of sub-tenants' resources. FusionInsight Manager supports setting of the administrator for a single tenant so that the management over this tenant can be delegated to a user who is not the system administrator.
-  Roles of a tenant have all permissions on the computing resources and storage resources of the tenant. When a tenant is created, the system automatically creates roles for this tenant. You can add a user and bind the user to the tenant roles so that the user can use the resources of the tenant.

Clear Resource Management
-------------------------

-  **Self-Service Resource Configuration**

   In FusionInsight Manager, you can configure the computing resources and storage resources during the creation of a tenant and add, modify, or delete the resources of the tenant.

   Permissions of the roles that are associated with a tenant are updated automatically when you modify the computing or storage resources of the tenant.

-  **Resource Usage Statistics**

   Resource usage statistics are critical for administrators to determine O&M activities based on the status of cluster applications and services, improving the cluster O&M efficiency. FusionInsight Manager displays the resource statistics of tenants in **Resource Quota**, including the vCores, memory, and HDFS storage resources.

   .. note::

      -  **Resource Quota** dynamically calculates the resource usage of tenants.

         |image1|

         The available resources of the Superior scheduler are calculated as follows:

         -  Superior

            The available Yarn resources (memory and CPU) are allocated in proportion based on the queue weight.

      -  When the tenant administrator is bound to a tenant role, the tenant administrator has the permissions to manage the tenant and use all resources of the tenant.

-  **Graphical Resource Monitoring**

   Graphical resource monitoring supports the graphical display of monitoring metrics listed in :ref:`Table 1 <admin_guide_000091__table3621114917574>`, as shown in :ref:`Figure 2 <admin_guide_000091__fig136061232032>`.

   .. _admin_guide_000091__fig136061232032:

   .. figure:: /_static/images/en-us_image_0263899641.png
      :alt: **Figure 2** Refined monitoring

      **Figure 2** Refined monitoring

   By default, the real-time monitoring data is displayed. You can click |image2| to customize a time range. The default time ranges include 4 hours, 8 hours, 12 hours, 1 day, 1 week, and 1 month. Click |image3| and select **Export** to export the monitoring metric information.

   .. _admin_guide_000091__table3621114917574:

   .. table:: **Table 1** Monitoring metrics

      +-----------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Service               | Metric Item                             | Description                                                                                                                                     |
      +=======================+=========================================+=================================================================================================================================================+
      | HDFS                  | HDFS Tenant Space Details               | HDFS can monitor a specified storage directory. The storage directory is the same as the directory added by the current tenant in **Resource**. |
      |                       |                                         |                                                                                                                                                 |
      |                       | -  Allocated Space                      |                                                                                                                                                 |
      |                       | -  Used Space                           |                                                                                                                                                 |
      +-----------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HDFS Tenant File Object Details         |                                                                                                                                                 |
      |                       |                                         |                                                                                                                                                 |
      |                       | -  Number of Used File Objects          |                                                                                                                                                 |
      +-----------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Yarn                  | Yarn Allocated Cores                    | Monitoring information of the current tenant is displayed. If no sub-item is configured for a tenant, this information is not displayed.        |
      |                       |                                         |                                                                                                                                                 |
      |                       | -  Maximum Number of CPU Cores in an AM | The monitoring data is obtained from **Scheduler** > **Application Queues** > **Queue:** *Tenant name* on the native web UI of Yarn.            |
      |                       | -  Allocated Cores                      |                                                                                                                                                 |
      |                       | -  Number of Used CPU Cores in an AM    |                                                                                                                                                 |
      +-----------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Yarn Allocated Memory                   |                                                                                                                                                 |
      |                       |                                         |                                                                                                                                                 |
      |                       | -  Allocated Maximum AM Memory          |                                                                                                                                                 |
      |                       | -  Allocated Memory                     |                                                                                                                                                 |
      |                       | -  Used AM Memory                       |                                                                                                                                                 |
      +-----------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001169371695.png
.. |image2| image:: /_static/images/en-us_image_0000001370085637.png
.. |image3| image:: /_static/images/en-us_image_0263899288.png
