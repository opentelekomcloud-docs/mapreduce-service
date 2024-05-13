:original_name: admin_guide_000018.html

.. _admin_guide_000018:

Static Service Resources
========================

Overview
--------

A cluster allocates static service resources to services Flume, HBase, HDFS, and YARN. The total volume of computing resources allocated to each service is fixed, and they are static. A tenant can exclusively use or share a service to obtain the resources required for running this service.

Static Service Pool
-------------------

Static service pools are used to specify service resource configurations.

Static service pools centrally manage resources that can be used by each service.

-  Limits the total number of resources that can be used by each services. Specifically, the total number of CPU, I/O, and memory resources can be configured on the nodes where services Flume, HBase, HDFS, and YARN are deployed.
-  Isolates the resources of services in a cluster from those of other services. In this way, the load of one service has very limited impact on other services.

Scheduling Mechanism
--------------------

The time-based dynamic resource scheduling mechanism enables different volumes of static resources to be configured for services at different time, optimizing service running environments and improving the cluster efficiency.

In a complex cluster environment, multiple services share resources in the cluster, but the resource service period of each service may be different.

The following use a bank customer as an example:

-  The HBase query service is heavy in the daytime.
-  The query service is light, but the Hive analysis service is heavy at night.

If fixed resources are allocated to each service, the following problems may occur:

-  The query service cannot obtain sufficient resources while the resources for the analysis service are idle in the daytime.
-  The analysis service cannot obtain sufficient resources while the resources for the query service are idle at night.

As a result, the cluster resource utilization is low and the service capability is weak. Resolve the problem in the following ways:

-  Sufficient resources need to be configured for HBase in the daytime.
-  Sufficient resources need to be configured for Hive at night.

The time-based dynamic scheduling mechanism can efficiently utilize resources and run tasks.
