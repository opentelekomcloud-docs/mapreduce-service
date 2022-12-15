:original_name: admin_guide_000130.html

.. _admin_guide_000130:

Configuring a Queue
===================

Scenario
--------

You can modify the queue configurations for a specified tenant on FusionInsight Manager.

Prerequisites
-------------

A tenant who uses the Capacity scheduler has been added.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Tenant Resources** > **Dynamic Resource Plan**.

   The **Resource Distribution Policy** page is displayed by default.

#. Click the **Queue Configurations** tab.

#. Set **Cluster** to the name of the target cluster. In **All tenants resources** area, locate the row that contains the target tenant resource and click **Modify** in the **Operation** column.

   .. note::

      -  You can also access the **Modify Queue Configuration** page as follows: In the tenant list on the **Tenant Resources Management** page, click the target tenant, click the **Resource** tab, and click |image1| next to **Queue Configurations (**\ *Queue name*\ **)**.
      -  A queue can be bound to only one non-default resource pool. That is, a newly added resource pool can be bound to only one queue to serve as the default resource pool of the queue.

   .. table:: **Table 1** Queue configuration parameters

      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                             |
      +===============================================+=========================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | Tenant Resources Name (Queue)                 | Indicates the tenant name and queue name.                                                                                                                                                                                                                                                                                                                                                                                               |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Maximum Applications                          | Indicates the maximum number of applications.                                                                                                                                                                                                                                                                                                                                                                                           |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Maximum AM Resource Percent                   | Indicates the maximum percentage of resources that can be used to run the ApplicationMaster in a cluster.                                                                                                                                                                                                                                                                                                                               |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Minimum User Resource Upper-Limit Percent (%) | Indicates the minimum resource guarantee (percentage) of a user. The resources for each user in a queue are limited at any time. If applications of multiple users are running at the same time in a queue, the resource usage of each user fluctuates between the minimum value and the maximum value. The minimum value is determined by the number of running applications, while the maximum value is determined by this parameter. |
      |                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
      |                                               | For example, assume that this parameter is set to **25**. If two users submit applications to the queue, each user can use a maximum of 50% resources; if three users submit applications to the queue, each user can use a maximum of 33% resources; if four users submit applications to the queue, each user can use a maximum of 25% resources.                                                                                     |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Resource Upper-Limit Factor              | Indicates the limit factor of the maximum user resource usage. The maximum user resource usage percentage can be obtained by multiplying the limit factor with the percentage of the tenant's actual resource usage in the cluster.                                                                                                                                                                                                     |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Status                                        | Indicates the current status of a resource plan. The value can be **Running** or **Stopped**.                                                                                                                                                                                                                                                                                                                                           |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool                         | Indicates the resource pool used by the queue. The default value is **default**.                                                                                                                                                                                                                                                                                                                                                        |
      |                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
      |                                               | If you want to change the resource pool, configure the queue capacity first. For details, see :ref:`Configuring the Queue Capacity Policy of a Resource Pool <admin_guide_000131>`.                                                                                                                                                                                                                                                     |
      +-----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001369765657.png
