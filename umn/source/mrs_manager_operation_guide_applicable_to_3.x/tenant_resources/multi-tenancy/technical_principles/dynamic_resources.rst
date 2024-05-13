:original_name: admin_guide_000094.html

.. _admin_guide_000094:

Dynamic Resources
=================

Overview
--------

Yarn provides distributed resource management for a big data cluster. The total volume of resources allocated to Yarn can be configured. Then Yarn allocates and schedules computing resources for job queues. The computing resources of MapReduce, Spark, Flink, and Hive job queues are allocated and scheduled by Yarn.

Yarn queues are fundamental units of scheduling computing resources.

The resources obtained by tenants using Yarn queues are dynamic resources. Users can dynamically create and modify the queue quotas and view the status and statistics of the queues.

Resource Pools
--------------

Nowadays, enterprise IT systems often face complex cluster environments and diverse upper-layer requirements. For example:

-  Heterogeneous cluster: The computing speed, storage capacity, and network performance of each node in the cluster are different. All the tasks of complex applications need to be properly allocated to each compute node in the cluster based on service requirements.
-  Computing isolation: Data must be shared among multiple departments but computing resources must be distributed onto different compute nodes.

These require that the compute nodes be further partitioned.

Resource pools are used to specify the configuration of dynamic resources. Yarn queues are associated with resource pools for resource allocation and scheduling.

One tenant can have only one default resource pool. Users can be bound to the role of a tenant to use the resources in the resource pool of the tenant. To use resources in multiple resource pools, a user can be bound to roles of multiple tenants.

Scheduling Mechanism
--------------------

Yarn dynamic resources support label-based scheduling. This policy creates labels for compute nodes (Yarn NodeManagers) and adds the compute nodes with the same label into the same resource pool. Then Yarn dynamically associates the queues with resource pools based on the resource requirements of the queues.

For example, a cluster has more than 40 nodes which are labeled by **Normal**, **HighCPU**, **HighMEM**, or **HighIO** based on their hardware and network configurations and added into four resource pools, respectively. :ref:`Table 1 <admin_guide_000094__t88a97f43aa8049388a46adeaaa2b19cc>` describes the performance of each node in the resource pool.

.. _admin_guide_000094__t88a97f43aa8049388a46adeaaa2b19cc:

.. table:: **Table 1** Performance of each node in a resource pool

   +---------+-----------------+------------------------------------+-----------------+---------------------------+
   | Label   | Number of Nodes | Hardware and Network Configuration | Added To        | Associated With           |
   +=========+=================+====================================+=================+===========================+
   | Normal  | 10              | General                            | Resource pool A | Common queue              |
   +---------+-----------------+------------------------------------+-----------------+---------------------------+
   | HighCPU | 10              | High-performance CPU               | Resource pool B | Computing-intensive queue |
   +---------+-----------------+------------------------------------+-----------------+---------------------------+
   | HighMEM | 10              | Large memory                       | Resource pool C | Memory-intensive queue    |
   +---------+-----------------+------------------------------------+-----------------+---------------------------+
   | HighIO  | 10              | High-performance network           | Resource pool D | I/O-intensive queue       |
   +---------+-----------------+------------------------------------+-----------------+---------------------------+

A queue can use only the compute nodes in its associated resource pool.

-  A common queue is associated with resource pool A and uses **Normal** nodes with general hardware and network configurations.
-  A computing-intensive queue is associated with resource pool B and uses **HighCPU** nodes with high-performance CPUs.
-  A memory-intensive queue is associated with resource pool C and uses **HighMEM** nodes with large memory.
-  An I/O-intensive queue is associated with resource pool C and uses **HighIO** nodes with high-performance network.

Yarn queues are associated with specified resource pools to efficiently utilize resources in resource pools and maximize node performance.

MRS Manager supports a maximum of 50 resource pools. The system has a default resource pool.

Schedulers
----------

By default, the Superior scheduler is enabled for the MRS cluster.

-  The Superior scheduler is an enhanced version and named after the Lake Superior, indicating that the scheduler can manage a large amount of data.

To meet enterprise requirements and tackle scheduling challenges faced by the Yarn community, the Superior scheduler makes the following enhancements:

-  Enhanced resource sharing policy

   The Superior scheduler supports queue hierarchy. It integrates the functions of open-source schedulers and shares resources based on configurable policies. In terms of instances, administrators can use the Superior scheduler to configure an absolute value or percentage policy for queue resources. The resource sharing policy of the Superior scheduler enhances label-based scheduling of Yarn as a resource pool feature. The nodes in the Yarn cluster can be grouped based on the capacity or service type to ensure that queues can more efficiently utilize resources.

-  Tenant-based resource reservation policy

   Some tenants may run critical tasks at some time, and their resource requirements must be preferentially addressed. The Superior scheduler builds a mechanism to support the resource reservation policy. Reserved resources can be allocated to the critical tasks running in the specified tenant queues in a timely manner to ensure proper task execution.

-  Fair sharing among tenants and resource pool users

   The Superior scheduler allows shared resources to be configured for users in a queue. Each tenant may have users with different weights. Heavily weighted users may require more shared resources.

-  Ensured scheduling performance in a big cluster

   The Superior scheduler receives heartbeats from each NodeManager and saves resource information in memory, which enables the scheduler to control cluster resource usage globally. The Superior scheduler uses the push scheduling model, which makes the scheduling more precise and efficient and remarkably improves cluster resource utilization. Additionally, the Superior scheduler delivers excellent performance when the interval between NodeManager heartbeats is long and prevents heartbeat storms in big clusters.

-  Priority policy

   If the minimum resource requirement of a service cannot be met after the service obtains all available resources, a preemption occurs. The preemption function is disabled by default.
