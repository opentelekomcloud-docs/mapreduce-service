:original_name: mrs_01_1734.html

.. _mrs_01_1734:

Viewing the Instance Monitoring Page
====================================

Scenarios
---------

On the HetuEngine web UI, you can view the detailed information about a specified service, including the execution status of each SQL statement. If the current cluster uses dual planes, a Windows host that can connect to the cluster service plane is required.

.. note::

   You cannot view the compute instance task monitoring page using Internet Explorer.

Prerequisites
-------------

You have created an administrator for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to FusionInsight Manager as an administrator who can access the HetuEngine web UI and choose **Cluster** > *Name of the desired cluster* > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.

#. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

#. Locate the row of the target **Instance ID**, and click **LINK** in the **WebUI** column of the row. The compute instance task monitoring page is displayed on a new page. The **Query History** page is displayed for the first access. Click **Metrics** to view the compute instance task monitoring page.


   .. figure:: /_static/images/en-us_image_0000001348740049.png
      :alt: **Figure 1** Compute instance task monitoring page

      **Figure 1** Compute instance task monitoring page

   .. table:: **Table 1** Metric description

      +---------------------------+--------------------------------------------------------------------------------------------+
      | Metric                    | Description                                                                                |
      +===========================+============================================================================================+
      | Cluster CPU Usage         | Indicates the CPU usage of the current instance.                                           |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Cluster Free Memory       | Indicates the free memory of the current instance.                                         |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Average Cluster CPU Usage | Indicates the average CPU usage of the current instance.                                   |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Used Query Memory         | Indicates the memory used by the current instance.                                         |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Running Queries           | Indicates the number of tasks concurrently executed on the current instance.               |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Queued Queries            | Indicates the number of tasks to be executed in the waiting queue on the current instance. |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Blocked Queries           | Indicates the number of blocked tasks on the current instance.                             |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Active Workers            | Indicates the number of valid Workers on the current instance.                             |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Avg Running Tasks         | Indicates the average number of running tasks in the current instance.                     |
      +---------------------------+--------------------------------------------------------------------------------------------+
      | Avg CPU cycles per worker | Indicates the average CPU cycles of each Worker on the current instance.                   |
      +---------------------------+--------------------------------------------------------------------------------------------+

#. Filter query tasks by **State** on the page.


   .. figure:: /_static/images/en-us_image_0000001296060020.png
      :alt: **Figure 2** Filtering tasks by **State**

      **Figure 2** Filtering tasks by **State**

   .. table:: **Table 2** State description

      +-----------------------+-------------------------------------------------------------+
      | State                 | Description                                                 |
      +=======================+=============================================================+
      | Select All            | Views tasks of all statuses.                                |
      +-----------------------+-------------------------------------------------------------+
      | Queued                | Views the tasks to be executed in the waiting queue.        |
      +-----------------------+-------------------------------------------------------------+
      | Waiting For Resources | Views the tasks that wait for resources.                    |
      +-----------------------+-------------------------------------------------------------+
      | Dispatching           | Views the tasks that are being dispatched.                  |
      +-----------------------+-------------------------------------------------------------+
      | Planning              | Views the tasks that are being planned.                     |
      +-----------------------+-------------------------------------------------------------+
      | Starting              | Views the tasks that start running.                         |
      +-----------------------+-------------------------------------------------------------+
      | Running               | Views running tasks.                                        |
      +-----------------------+-------------------------------------------------------------+
      | Finishing             | Views the tasks that are being finished.                    |
      +-----------------------+-------------------------------------------------------------+
      | Finished              | Views the finished tasks.                                   |
      +-----------------------+-------------------------------------------------------------+
      | Failed                | Views failed tasks, which can be filtered by failure cause. |
      +-----------------------+-------------------------------------------------------------+

#. Click a task ID to view the basic information, resource usage, stages, and tasks. For a failed task, you can view related logs on the detail query page.


   .. figure:: /_static/images/en-us_image_0000001348740045.png
      :alt: **Figure 3** Viewing task details

      **Figure 3** Viewing task details


   .. figure:: /_static/images/en-us_image_0000001349059865.png
      :alt: **Figure 4** Task resource utilization summary

      **Figure 4** Task resource utilization summary


   .. figure:: /_static/images/en-us_image_0000001349139733.png
      :alt: **Figure 5** Stages

      **Figure 5** Stages

   .. table:: **Table 3** Stages monitoring information

      +---------------------+--------------------------------------------------------------------------------------+
      | Monitoring Item     | Description                                                                          |
      +=====================+======================================================================================+
      | SCHEDULED TIME SKEW | Indicates the scheduled time of the concurrent tasks on a node in the current stage. |
      +---------------------+--------------------------------------------------------------------------------------+
      | CPU TIME SKEW       | Indicates whether concurrent tasks have computing skew in any stage phase.           |
      +---------------------+--------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000001349139729.png
      :alt: **Figure 6** Tasks

      **Figure 6** Tasks

   .. table:: **Table 4** **Tasks** monitoring items

      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Monitoring Item | Description                                                                                                                                                                                                                                                             |
      +=================+=========================================================================================================================================================================================================================================================================+
      | ID              | Indicates the ID of the task that is concurrently executed in multiple phases. The format is *Stage ID*:*Task ID*.                                                                                                                                                      |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Host            | Indicates the Worker node where the current task is being executed.                                                                                                                                                                                                     |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | State           | Indicates the task execution status, including **PLANNED**, **RUNNING**, **FINISHED**, **CANCELED**, **ABORTED**, and **FAILED**.                                                                                                                                       |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Rows            | Indicates the total number of data records read by a task. The unit is thousand (k) or million (M). By analyzing the number of data records read by different tasks in the same stage, you can quickly determine whether data skew occurs in the current task.          |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Rows/s          | Indicates the number of data records read by a task per second. By analyzing the number of data records read by different tasks in the same stage, you can quickly determine whether the network bandwidth of the node is different and whether the node NIC is faulty. |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bytes           | Indicates the data volume read by a task.                                                                                                                                                                                                                               |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bytes/s         | Indicates the data volume read by a task per second.                                                                                                                                                                                                                    |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Elapsed         | Indicates the task execution duration.                                                                                                                                                                                                                                  |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | CPU Time        | Indicates the CPU time used by a task.                                                                                                                                                                                                                                  |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Buffered        | Indicates the buffer size of a task.                                                                                                                                                                                                                                    |
      +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click the "Host" link to view the task resource usage of each node.


   .. figure:: /_static/images/en-us_image_0000001349259313.png
      :alt: **Figure 7** Resource usage of the Task node

      **Figure 7** Resource usage of the Task node

   .. table:: **Table 5** Monitoring metrics of node resources

      +-------------------------+------------------------------------------------------------+
      | Name                    | Description                                                |
      +=========================+============================================================+
      | Node ID                 | Indicates the host ID.                                     |
      +-------------------------+------------------------------------------------------------+
      | Heap Memory             | Indicates the maximum heap memory size.                    |
      +-------------------------+------------------------------------------------------------+
      | Processors              | Indicates the number of processors.                        |
      +-------------------------+------------------------------------------------------------+
      | Uptime                  | Indicates the running duration.                            |
      +-------------------------+------------------------------------------------------------+
      | External Address        | Indicates the external IP address.                         |
      +-------------------------+------------------------------------------------------------+
      | Internal Address        | Indicates the internal IP address.                         |
      +-------------------------+------------------------------------------------------------+
      | Process CPU Utilization | Indicates the physical CPU utilization.                    |
      +-------------------------+------------------------------------------------------------+
      | System CPU Utilization  | Indicates the system CPU utilization.                      |
      +-------------------------+------------------------------------------------------------+
      | Heap Utilization        | Indicates the heap memory utilization.                     |
      +-------------------------+------------------------------------------------------------+
      | Non-Heap Memory Used    | Indicates the non-Heap memory size.                        |
      +-------------------------+------------------------------------------------------------+
      | Memory Pools            | Indicates the memory pool size of the current Worker node. |
      +-------------------------+------------------------------------------------------------+
