:original_name: admin_guide_000112.html

.. _admin_guide_000112:

Configuring a Queue
===================

Scenario
--------

You can modify the queue configurations for a specified tenant on FusionInsight Manager.

Prerequisites
-------------

A tenant who uses the Superior scheduler has been added.

Procedure
---------

#. On FusionInsight Manager, choose **Tenant Resources**.
#. Choose **Dynamic Resource Plan**.
#. Click the **Queue Configurations** tab.
#. Set **Cluster** to the name of the target cluster. In **All tenants resources** area, locate the row that contains the target tenant resource and click **Modify** in the **Operation** column.

   .. note::

      -  You can also access the **Modify Queue Configuration** page as follows: In the tenant list on the **Tenant Resources Management** page, click the target tenant, click the **Resource** tab, and click |image1| next to **Queue Configurations (Queue name)**.
      -  A queue can be bound to only one non-default resource pool.
      -  For parameters such as **Max Allocated vCores**, **Max Allocated Memory(MB)**, **Max Running Apps**, **Max Running Apps per User**, and **Max Pending Apps**, if the value of a sub-tenant is **-1**, the value of the parent tenant can be set to a specific limit. If the parent tenant value is a specific limit, the sub-tenant value can be set to **-1**.
      -  **Max Allocated vCores** and **Max Allocated Memory(MB)** must be both changed to values other than **-1**.

   .. table:: **Table 1** Queue configuration parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================================================================================================================================================================+
      | Max Master Shares(%)              | Indicates the maximum percentage of resources occupied by all ApplicationMasters in the current queue.                                                                                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Allocated vCores              | Indicates the maximum number of cores that can be allocated to a single Yarn container in the current queue. The default value is **-1**, indicating that the number of cores is not limited within the value range.                                                                                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Allocated Memory(MB)          | Indicates the maximum memory that can be allocated to a single Yarn container in the current queue. The default value is **-1**, indicating that the memory is not limited within the value range.                                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Running Apps                  | Indicates the maximum number of tasks that can be executed at the same time in the current queue. The default value is **-1**, indicating that the number is not limited within the value range (the meaning is the same if the value is empty). Value **0** indicates that tasks cannot be executed. The value ranges from **-1** to **2147483647**.              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Running Apps per User         | Indicates the maximum number of tasks that can be executed by each user in the current queue at the same time. The default value is **-1**, indicating that the number is not limited within the value range (the meaning is the same if the value is empty). Value **0** indicates that tasks cannot be executed. The value ranges from **-1** to **2147483647**. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Pending Apps                  | Indicates the maximum number of tasks that can be suspended at the same time in the current queue. The default value is **-1**, indicating that the number is not limited within the value range (the meaning is the same if the value is empty). Value **0** indicates that tasks cannot be suspended. The value ranges from **-1** to **2147483647**.            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resource Allocation Rule          | Indicates the rule for allocating resources to different tasks of a user. The rule can be **FIFO** or **FAIR**.                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | If a user submits multiple tasks in the current queue and the rule is **FIFO**, the tasks are executed one by one in sequential order; If the rule is **FAIR**, resources are evenly allocated to all tasks.                                                                                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Label            | Indicates that tasks are executed on a node with a specified resource label.                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Active                            | -  **ACTIVE**: indicates that the current queue can receive and execute tasks.                                                                                                                                                                                                                                                                                     |
      |                                   | -  **INACTIVE**: indicates that the current queue can receive but cannot execute tasks. Tasks submitted to the queue are suspended.                                                                                                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Open                              | -  **OPEN**: indicates that the current queue is opened.                                                                                                                                                                                                                                                                                                           |
      |                                   | -  **CLOSED**: indicates that the current queue is closed. Tasks submitted to the queue are rejected.                                                                                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Migrate Queue Upon Fault          | If cross-AZ HA is enabled for a cluster and an AZ is faulty, set **Migrate Queue Upon Fault** to **TRUE** to migrate running queues of the tenant to other AZs.                                                                                                                                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001442494093.png
