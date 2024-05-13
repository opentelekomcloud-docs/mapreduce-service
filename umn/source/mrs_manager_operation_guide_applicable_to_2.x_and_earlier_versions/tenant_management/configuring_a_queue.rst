:original_name: mrs_01_0547.html

.. _mrs_01_0547:

Configuring a Queue
===================

Scenario
--------

This section describes how to modify the queue configuration for a specified tenant on MRS Manager.

Prerequisites
-------------

A tenant associated with Yarn and allocated dynamic resources has been added.

Procedure
---------

#. On MRS Manager, click **Tenant**.
#. Click the **Dynamic Resource Plan** tab.
#. Click the **Queue Configuration** tab.
#. In the tenant queue table, click **Modify** in the **Operation** column of the specified tenant queue.

   .. note::

      In the tenant list on the left of the **Tenant Management** tab, click the target tenant. In the window that is displayed, choose **Resource**. On the page that is displayed, click |image1| to open the queue modification page.

   .. table:: **Table 1** Queue configuration parameters

      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                      | Description                                                                                                                                                                                                                                                     |
      +================================+=================================================================================================================================================================================================================================================================+
      | Maximum Application            | Specifies the maximum number of applications. The value ranges from 1 to 2147483647.                                                                                                                                                                            |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Maximum AM Resource Percent    | Specifies the maximum percentage of resources that can be used to run the ApplicationMaster in a cluster. The value ranges from 0 to 1.                                                                                                                         |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Minimum User Limit Percent (%) | Specifies the minimum percentage of resources consumed by a user. The value ranges from 0 to 100.                                                                                                                                                               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Limit Factor              | Specifies the limit factor of the maximum user resource usage. The maximum user resource usage percentage can be obtained by multiplying the limit factor with the percentage of the tenant's actual resource usage in the cluster. The minimum value is **0**. |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Status                         | Specifies the current status of a resource plan. The values are **Running** and **Stopped**.                                                                                                                                                                    |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Default Resource Pool          | Specifies the resource pool used by a queue. The default value is **Default**. If you want to change the resource pool, configure the queue capacity first. For details, see :ref:`Configuring the Queue Capacity Policy of a Resource Pool <mrs_01_0548>`.     |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001782347050.png
