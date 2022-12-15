:original_name: mrs_08_00514.html

.. _mrs_08_00514:

Yarn Enhanced Open Source Features
==================================

Priority-based task scheduling
------------------------------

In the native Yarn resource scheduling mechanism, if the whole Hadoop cluster resources are occupied by those MapReduce jobs submitted earlier, jobs submitted later will be kept in pending state until all running jobs are executed and resources are released.

The MRS cluster provides the task priority scheduling mechanism. With this feature, you can define jobs of different priorities. Jobs of high priority can preempt resources released from jobs of low priority though the high-priority jobs are submitted later. The low-priority jobs that are not started will be suspended unless those jobs of high priority are completed and resources are released, then they can properly be started.

This feature enables services to control computing jobs more flexibly, thereby achieving higher cluster resource utilization.

.. note::

   Container reuse is in conflict with task priority scheduling. If container reuse is enabled, resources are being occupied, and task priority scheduling does not take effect.

Yarn Permission Control
-----------------------

The permission mechanism of Hadoop Yarn is implemented through ACLs. The following describes how to grant different permission control to different users:

-  Admin ACL

   An O&M administrator is specified for the Yarn cluster. The Admin ACL is determined by **yarn.admin.acl**. The cluster O&M administrator can access the ResourceManager web UI and operate NodeManager nodes, queues, and NodeLabel, **but cannot submit tasks**.

-  Queue ACL

   To facilitate user management in the cluster, users or user groups are divided into several queues to which each user and user group belongs. Each queue contains permissions to submit and manage applications (for example, terminate any application).

Open source functions:

Currently, Yarn supports the following roles for users:

-  Cluster O&M administrator
-  Queue administrator
-  Common user

However, the APIs (such as the web UI, REST API, and Java API) provided by Yarn do not support role-specific permission control. Therefore, all users have the permission to access the application and cluster information, which does not meet the isolation requirements in the multi-tenant scenario.

This is an enhanced function.

In security mode, permission management is enhanced for the APIs such as web UI, REST API, and Java API provided by Yarn. Permission control can be performed based on user roles.

Role-based permissions are as follows:

-  Cluster O&M administrator: performs management operations in the Yarn cluster, such as accessing the ResourceManager web UI, refreshing queues, setting NodeLabel, and performing active/standby switchover.
-  Queue administrator: has the permission to modify and view queues managed by the Yarn cluster.
-  Common user: has the permission to modify and view self-submitted applications in the Yarn cluster.

Superior Scheduler Principle (Self-developed)
---------------------------------------------

Superior Scheduler is a scheduling engine designed for the Hadoop Yarn distributed resource management system. It is a high-performance and enterprise-level scheduler designed for converged resource pools and multi-tenant service requirements.

Superior Scheduler achieves all functions of open source schedulers, Fair Scheduler, and Capacity Scheduler. Compared with the open source schedulers, Superior Scheduler is enhanced in the enterprise multi-tenant resource scheduling policy, resource isolation and sharing among users in a tenant, scheduling performance, system resource usage, and cluster scalability. Superior Scheduler is designed to replace open source schedulers.

Similar to open source Fair Scheduler and Capacity Scheduler, Superior Scheduler follows the Yarn scheduler plugin API to interact with Yarn ResourceManager to offer resource scheduling functionalities. :ref:`Figure 1 <mrs_08_00514__f6e2f095c1ef043d0ba716e26731052b3>` shows the overall system diagram.

.. _mrs_08_00514__f6e2f095c1ef043d0ba716e26731052b3:

.. figure:: /_static/images/en-us_image_0000001296430794.jpg
   :alt: **Figure 1** Internal architecture of Superior Scheduler

   **Figure 1** Internal architecture of Superior Scheduler

In :ref:`Figure 1 <mrs_08_00514__f6e2f095c1ef043d0ba716e26731052b3>`, Superior Scheduler consists of the following modules:

-  Superior Scheduler Engine is a high performance scheduler engine with rich scheduling policies.

-  Superior Yarn Scheduler Plugin functions as a bridge between Yarn ResourceManager and Superior Scheduler Engine and interacts with Yarn ResourceManager.

   The scheduling principle of open source schedulers is that resources match jobs based on the heartbeats of computing nodes. Specifically, each computing node periodically sends heartbeat messages to ResourceManager of Yarn to notify the node status and starts the scheduler to assign jobs to the node itself. In this scheduling mechanism, the scheduling period depends on the heartbeat. If the cluster scale increases, bottleneck on system scalability and scheduling performance may occur. In addition, because resources match jobs, the scheduling accuracy of an open source scheduler is limited. For example, data affinity is random and the system does not support load-based scheduling policies. The scheduler may not make the best choice due to lack of the global resource view when selecting jobs.

   Superior Scheduler adopts multiple scheduling mechanisms. There are dedicated scheduling threads in Superior Scheduler, separating heartbeats with scheduling and preventing system heartbeat storms. Additionally, Superior Scheduler matches jobs with resources, providing each scheduled job with a global resource view and increasing the scheduling accuracy. Compared with the open source scheduler, Superior Scheduler excels in system throughput, resource usage, and data affinity.


.. figure:: /_static/images/en-us_image_0000001349110493.png
   :alt: **Figure 2** Comparison of Superior Scheduler with open source schedulers

   **Figure 2** Comparison of Superior Scheduler with open source schedulers

Apart from the enhanced system throughput and utilization, Superior Scheduler provides following major scheduling features:

-  Multiple resource pools

   Multiple resource pools help logically divide cluster resources and share them among multiple tenants or queues. The division of resource pools supports heterogeneous resources. Resource pools can be divided exactly according to requirements on the application resource isolation. You can configure further policies for different queues in a pool.

-  Multi-tenant scheduling (**reserve**, **min**, **share**, and **max**) in each resource pool

   Superior Scheduler provides flexible hierarchical multi-tenant scheduling policy. Different policies can be configured for different tenants or queues that can access different resource pools. The following figure lists supported policies:

   .. table:: **Table 1** Policy description

      +---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Name    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
      +=========+=================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | reserve | This policy is used to reserve resources for a tenant. Even though tenant has no jobs available, other tenant cannot use the reserved resource. The value can be a percentage or an absolute value. If both the percentage and absolute value are configured, the percentage is automatically calculated into an absolute value, and the larger value is used. The default **reserve** value is **0**. Compared with the method of specifying a dedicated resource pool and hosts, the **reserve** policy provides a flexible floating reservation function. In addition, because no specific hosts are specified, the data affinity for calculation is improved and the impact by the faulty hosts is avoided. |
      +---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | min     | This policy allows preemption of minimum resources. Other tenants can use these resources, but the current tenant has the priority to use them. The value can be a percentage or an absolute value. If both the percentage and absolute value are configured, the percentage is automatically calculated into an absolute value, and the larger value is used. The default value is **0**.                                                                                                                                                                                                                                                                                                                      |
      +---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | share   | This policy is used for shared resources that cannot be preempted. To use these resources, the current tenant needs to wait for other tenants to complete jobs and release resources. The value can be a percentage or an absolute value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
      +---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | max     | This policy is used for the maximum resources that can be utilized. The tenant cannot obtain more resources than the allowed maximum value. The value can be a percentage or an absolute value. If both the percentage and absolute value are configured, the percentage is automatically calculated into an absolute value, and the larger value is used. By default value, there is no restriction on resources.                                                                                                                                                                                                                                                                                              |
      +---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   :ref:`Figure 3 <mrs_08_00514__fe57392ff64944567bd0cb78bbc2aaeeb>` shows the tenant resource allocation policy.

   .. _mrs_08_00514__fe57392ff64944567bd0cb78bbc2aaeeb:

   .. figure:: /_static/images/en-us_image_0000001296590646.jpg
      :alt: **Figure 3** Resource scheduling policies

      **Figure 3** Resource scheduling policies

   .. note::

      In the above figure, **Total** indicates the total number of resources, not the scheduling policy.

   Compared with open source schedulers, Superior Scheduler supports both percentage and absolute value of tenants for allocating resources, flexibly addressing resource scheduling requirements of enterprise-level tenants. For example, resources can be allocated according to the absolute value of level-1 tenants, avoiding impact caused by changes of cluster scale. However, resources can be allocated according to the allocation percentage of sub-tenants, improving resource usages in the level-1 tenant.

-  Heterogeneous and multi-dimensional resource scheduling

   Superior Scheduler supports following functions except CPU and memory scheduling:

   -  `Node labels <https://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/NodeLabel.html>`__ can be used to identify multi-dimensional attributes of nodes such as **GPU_ENABLED** and **SSD_ENBALED**, and can be scheduled based on these labels.
   -  Resource pools can be used to group resources of the same type and allocate them to specific tenants or queues.

-  Fair scheduling of multiple users in a tenant

   In a leaf tenant, multiple users can use the same queue to submit jobs. Compared with the open source schedulers, Superior Scheduler supports configuring flexible resource sharing policy among different users in a same tenant. For example, VIP users can be configured with higher resource access weight.

-  Data locality aware scheduling

   Superior Scheduler adopts the job-to-node scheduling policy. That is, Superior Scheduler attempts to schedule specified jobs between available nodes so that the selected node is suitable for the specified jobs. By doing so, the scheduler will have an overall view of the cluster and data. Localization is ensured if there is an opportunity to place tasks closer to the data. The open source scheduler uses the node-to-job scheduling policy to match the appropriate jobs to a given node.

-  Dynamic resource reservation during container scheduling

   In a heterogeneous and diversified computing environment, some containers need more resources or multiple resources. For example, Spark job may require large memory. When such containers compete with containers requiring fewer resources, containers requiring more resources may not obtain sufficient resources within a reasonable period. Open source schedulers allocate resources to jobs, which may cause unreasonable resource reservation for these jobs. This mechanism leads to the waste of overall system resources. Superior Scheduler differs from open source schedulers in following aspects:

   -  Requirement-based matching: Superior Scheduler schedules jobs to nodes and selects appropriate nodes to reserve resources to improve the startup time of containers and avoid waste.
   -  Tenant rebalancing: When the reservation logic is enabled, the open source schedulers do not comply with the configured sharing policy. Superior Scheduler uses different methods. In each scheduling period, Superior Scheduler traverses all tenants and attempts to balance resources based on the multi-tenant policy. In addition, Superior Scheduler attempts to meet all policies (**reserve**, **min**, and **share**) to release reserved resources and direct available resources to other containers that should obtain resources under different tenants.

-  Dynamic queue status control (**Open**/**Closed**/**Active**/**Inactive**)

   Multiple queue statuses are supported, helping administrators operate and maintain multiple tenants.

   -  Open status (**Open/Closed**): If the status is **Open** by default, applications submitted to the queue are accepted. If the status is **Closed**, no application is accepted.
   -  Active status (**Active/Inactive**): If the status is **Active** by default, resources can be scheduled and allocated to applications in the tenant. Resources will not be scheduled to queues in **Inactive** status.

-  Application pending reason

   If the application is not started, provide the job pending reasons.

:ref:`Table 2 <mrs_08_00514__t233dcb46b3d246b38e43771ca2810229>` describes the comparison result of Superior Scheduler and Yarn open source schedulers.

.. _mrs_08_00514__t233dcb46b3d246b38e43771ca2810229:

.. table:: **Table 2** Comparative analysis

   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scheduling                                    | Yarn Open Source Scheduler                                                                                                                                                                                                                                   | Superior Scheduler                                                                                                                             |
   +===============================================+==============================================================================================================================================================================================================================================================+================================================================================================================================================+
   | Multi-tenant scheduling                       | In homogeneous clusters, either Capacity Scheduler or Fair Scheduler can be selected and the cluster does not support Fair Scheduler. Capacity Scheduler supports the scheduling by percentage and Fair Scheduler supports the scheduling by absolute value. | -  Supports heterogeneous clusters and multiple resource pools.                                                                                |
   |                                               |                                                                                                                                                                                                                                                              | -  Supports **reservation** to ensure direct access to resources.                                                                              |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Data locality aware scheduling                | The node-to-job scheduling policy reduces the success rate of data localization and potentially affects application execution performance.                                                                                                                   | The **job-to-node scheduling policy** can aware data location more accurately, and the job hit rate of data localization scheduling is higher. |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Balanced scheduling based on load of hosts    | Not supported                                                                                                                                                                                                                                                | **Balanced scheduling can be achieved when Superior Scheduler considers the host load and resource allocation during scheduling.**             |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Fair scheduling of multiple users in a tenant | Not supported                                                                                                                                                                                                                                                | Supports keywords **default** and **others**.                                                                                                  |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Job waiting reason                            | Not supported                                                                                                                                                                                                                                                | Job waiting reasons illustrate why a job needs to wait.                                                                                        |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

In conclusion, Superior Scheduler is a high-performance scheduler with various scheduling policies and is better than Capacity Scheduler in terms of functionality, performance, resource usage, and scalability.

CPU Hard Isolation
------------------

Yarn cannot strictly control the CPU resources used by each container. When the CPU subsystem is used, a container may occupy excessive resources. Therefore, CPUset is used to control resource allocation.

To solve this problem, the CPU resources are allocated to each container based on the ratio of virtual cores (vCores) to physical cores. If a container requires an entire physical core, the container has it. If a container needs only some physical cores, several containers may share the same physical core. The following figure shows an example of the CPU quota. The given ratio of vCores to physical cores is 2:1.


.. figure:: /_static/images/en-us_image_0000001296750262.png
   :alt: **Figure 4** CPU quota

   **Figure 4** CPU quota

Enhanced Open Source Feature: Optimizing Restart Performance
------------------------------------------------------------

Generally, the recovered ResourceManager can obtain running and completed applications. However, a large number of completed applications may cause problems such as slow startup and long HA switchover/restart time of ResourceManagers.

To speed up the startup, obtain the list of unfinished applications before starting the ResourceManagers. In this case, the completed application continues to be recovered in the background asynchronous thread. The following figure shows how the ResourceManager recovery starts.


.. figure:: /_static/images/en-us_image_0000001349190361.jpg
   :alt: **Figure 5** Starting the ResourceManager recovery

   **Figure 5** Starting the ResourceManager recovery
