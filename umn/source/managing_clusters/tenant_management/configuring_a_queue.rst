:original_name: mrs_01_0313.html

.. _mrs_01_0313:

Configuring a Queue
===================

Scenario
--------

You can modify the queue configuration of a specified tenant on MRS based on service requirements.

Prerequisites
-------------

-  A tenant associated with Yarn and allocated dynamic resources has been added.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Configuring a Queue <mrs_01_0547>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. Click the **Queue Configuration** tab.

#. In the tenant queue table, click **Modify** in the **Operation** column of the specified tenant queue.

   .. note::

      -  In the tenant list on the left of the **Tenant Management** tab, click the target tenant. In the window that is displayed, choose **Resource**. On the page that is displayed, click |image1| to open the queue modification page.
      -  A queue can be bound to only one non-default resource pool.

   Versions earlier than MRS 3.x:

   .. table:: **Table 1** Queue configuration parameters

      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                             | Description                                                                                                                                                                                                                                                     |
      +=======================================================+=================================================================================================================================================================================================================================================================+
      | Maximum Applications                                  | Specifies the maximum number of applications. The value ranges from 1 to 2147483647.                                                                                                                                                                            |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Maximum AM Resource Percent                           | Specifies the maximum percentage of resources that can be used to run the ApplicationMaster in a cluster. The value ranges from 0 to 1.                                                                                                                         |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Minimum User Limit Percent (%)                        | Specifies the minimum percentage of resources consumed by a user. The value ranges from 0 to 100.                                                                                                                                                               |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Limit Factor                                     | Specifies the limit factor of the maximum user resource usage. The maximum user resource usage percentage can be obtained by multiplying the limit factor with the percentage of the tenant's actual resource usage in the cluster. The minimum value is **0**. |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Status                                                | Specifies the current status of a resource plan. The values are **Running** and **Stopped**.                                                                                                                                                                    |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool (Default Node Label Expression) | Specifies the resource pool used by a queue. The default value is **default**. If you want to change the resource pool, configure the queue capacity first. For details, see :ref:`Configuring the Queue Capacity Policy of a Resource Pool <mrs_01_0314>`.     |
      +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   MRS 3.x or later:

   .. table:: **Table 2** Queue configuration parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                           |
      +===================================+=======================================================================================================================================================================================================================================================================================================================================+
      | Max Master Shares (%)             | Indicates the maximum percentage of resources occupied by all ApplicationMasters in the current queue.                                                                                                                                                                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Allocated vCores              | Indicates the maximum number of cores that can be allocated to a single YARN container in the current queue. The default value is **-1**, indicating that the number of cores is not limited within the value range.                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Allocated Memory (MB)         | Indicates the maximum memory that can be allocated to a single Yarn container in the current queue. The default value is **-1**, indicating that the memory is not limited within the value range.                                                                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Running Apps                  | Maximum number of tasks that can be executed at the same time in the current queue. The default value is **-1**, indicating that the number is not limited within the value range (the meaning is the same if the value is empty). The value 0 indicates that the task cannot be executed. The value ranges from -1 to 2147483647.    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Running Apps per User         | Maximum number of tasks that can be executed by each user in the current queue at the same time. The default value is **-1**, indicating that the number is not limited within the value range. If the value is **0**, the task cannot be executed. The value ranges from -1 to 2147483647.                                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max Pending Apps                  | Maximum number of tasks that can be suspended at the same time in the current queue. The default value is **-1**, indicating that the number is not limited within the value range (the meaning is the same if the value is empty). The value **0** indicates that tasks cannot be suspended. The value ranges from -1 to 2147483647. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resource Allocation Rule          | Indicates the rule for allocating resources to different tasks of a user. The rule can be FIFO or FAIR.                                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                                       |
      |                                   | If a user submits multiple tasks in the current queue and the rule is FIFO, the tasks are executed one by one in sequential order. If the rule is FAIR, resources are evenly allocated to all tasks.                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Label            | Indicates that tasks are executed on a node with a specified resource label.                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                       |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                                                       |
      |                                   |    If you need to use a new resource pool, change the default label to the new resource pool label.                                                                                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Active                            | -  **ACTIVE**: indicates that the current queue can receive and execute tasks.                                                                                                                                                                                                                                                        |
      |                                   | -  **INACTIVE**: indicates that the current queue can receive but cannot execute tasks. Tasks submitted to the queue are suspended.                                                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Open                              | -  **OPEN**: indicates that the current queue is opened.                                                                                                                                                                                                                                                                              |
      |                                   | -  **CLOSED**: indicates that the current queue is closed. Tasks submitted to the queue are rejected.                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001296057872.png
