:original_name: mrs_01_24790.html

.. _mrs_01_24790:

ClickHouse Multi-Tenancy Overview
=================================

.. note::

   This section applies only to MRS 3.2.0 or later.

ClickHouse Multi-Tenancy
------------------------

The ClickHouse multi-tenancy feature enables you to manage cluster resources through the user > tenant role > resource profile management model. Currently, memory and CPU priority management is supported. The following figure shows a multi-tenancy model.

|image1|

On the service configuration and tenant management pages of FusionInsight Manager, you can configure memory quotas for services, create tenants, associate ClickHouse services, bind logical clusters, set available memory and CPU priorities for tenants, and associate tenants with users. The following figure illustrates the role association between Manager and ClickHouse.

|image2|

The following table lists the resource configurations supported by the current version.

+-------------------------------------+-------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Resource                            | Value Range | Description                                                                                                      | Remarks                                                                                                                                                                                                                          |
+=====================================+=============+==================================================================================================================+==================================================================================================================================================================================================================================+
| Service-level memory resource limit | 0-1         | Percentage of available ClickHouse memory to total server memory                                                 | For example, if the physical memory of the server is 10 GB and the limit is set to **0.9**, the available memory of the ClickHouse service on the current server is 9 GB (10 GB x 0.9).                                          |
+-------------------------------------+-------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Tenant-level memory resource limit  | 0%-100%     | Percentage of the available memory of the current tenant in ClickHouseServer                                     | If this limit is set to **80**, the total memory that can be used by the current tenant is calculated as follows: Total memory that can be used by the service x 80%                                                             |
+-------------------------------------+-------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Tenant-level CPU priority           | -20 to 19   | NICE value of the OS associated with this value. A smaller value indicates a higher CPU priority of the process. | This feature depends on **CAP_SYS_NICE** of the OS. By default, this feature is disabled after the cluster is installed. To use this feature, enable it by referring to :ref:`Enabling the CPU Priority Feature <mrs_01_24789>`. |
+-------------------------------------+-------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001532836094.png
.. |image2| image:: /_static/images/en-us_image_0000001532996022.png
