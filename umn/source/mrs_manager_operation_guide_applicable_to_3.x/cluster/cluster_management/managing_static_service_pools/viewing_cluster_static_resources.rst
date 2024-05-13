:original_name: admin_guide_000020.html

.. _admin_guide_000020:

Viewing Cluster Static Resources
================================

Scenario
--------

The big data management platform can manage and isolate service resources that are not running on YARN using static service resource pools. The system supports time-based automatic adjustment of static service resource pools. This enables the cluster to automatically adjust the parameter values at different periods to ensure more efficient resource utilization.

System administrators can view the monitoring indicators of resources used by each service in the static service pool on MRS Manager. The monitoring indicators are as follows:

-  CPU usage of services
-  Total disk I/O read rate of services
-  Total disk I/O write rate of services
-  Total used memory of services

.. note::

   After the multi-tenant function is enabled, the CPU, I/O, and memory usage of all HBase instances can be centrally managed.

Procedure
---------

#. On MRS Manager, choose **Cluster**, click the name of the target cluster, and choose **Static Service Pool Configurations**.
#. In the configuration group list, click a configuration group, for example, **default**.
#. Check the system resource adjustment base values.

   -  **System Resource Adjustment Base** indicates the maximum volume of resources that can be used by each node in the cluster. If a node has only one service, the service exclusively occupies the available resources on the node. If a node has multiple services, all services share the available resources on the node.
   -  **CPU** indicates the maximum number of CPUs that can be used by services on a node.
   -  **Memory** indicates the maximum memory that can be used by services on a node.

#. In **Chart**, view the metric data of the cluster service resource usage.

   .. note::

      -  You can click **Add Service to Chart** to add static service resource data of specific services (up to 12 services) to the chart.
      -  For details about how to manage a chart, see :ref:`Managing Monitoring Metric Reports <admin_guide_000008>`.
