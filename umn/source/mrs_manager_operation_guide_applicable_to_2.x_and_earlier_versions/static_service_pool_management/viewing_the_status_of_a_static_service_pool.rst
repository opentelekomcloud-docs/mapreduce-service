:original_name: mrs_01_0535.html

.. _mrs_01_0535:

Viewing the Status of a Static Service Pool
===========================================

Scenario
--------

MRS Manager manages and isolates service resources that are not running on YARN through the static service resource pool. It dynamically manages the total CPU, I/O, and memory resources that can be used by HDFS and YARN on the deployment node. The system supports time-based automatic adjustment of static service resource pools. This enables the cluster to automatically adjust the parameter values at different periods to ensure more efficient resource utilization.

On MRS Manager, you can view the monitoring metrics of the resources used by each service in the static service pool. The monitoring metrics are as follows:

-  Service Total CPU Usage
-  Service Total Disk I/O Read Speed
-  Service Total Disk I/O Write Speed
-  Service Total Memory Usage

Procedure
---------

#. On MRS Manager, click **System**. In the **Resource** area, click **Configure Static Service Pool**.
#. Click **Status**.
#. Check the system resource adjustment base values.

   -  **System Resource Adjustment Base** indicates the maximum volume of resources that can be used by each node in the cluster. If a node has only one service, the service exclusively occupies the available resources on the node. If a node has multiple services, all services share the available resources on the node.
   -  **CPU(%)** indicates the maximum number of CPUs that can be used by services on a node.
   -  **Memory(%)** indicates the maximum memory that can be used by services on a node.

4.  Check the cluster service resource usage.

    In the chart area, select **All services** from the service drop-down list box. The resource usage status of all services in the service pool is displayed.

    .. note::

       **Effective Configuration Group** indicates the resource control configuration group used by the cluster service. By default, the **default** configuration group is used at all time every day, indicating that the cluster service can use all CPUs and 70% memory of the node.

5.  View the resource usage of a single service.

    In the chart area, select a service from the service drop-down list box. The resource usage status of the service is displayed.

6.  You can set the interval for automatically refreshing the page.

    The following refresh interval options are supported:

    -  **Refresh every 30 seconds**
    -  **Refresh every 60 seconds**
    -  **Stop refreshing**

7.  In the **Period** area, select a time range for viewing service resources. The options are as follows:

    -  Real time
    -  Last 3 hours
    -  Last 6 hours
    -  Last 24 hours
    -  Last week
    -  Last month
    -  Last 3 months
    -  Last 6 months
    -  Customize: If you select this option, you can customize the period for viewing monitoring data.

8.  Click **View** to view the service resource data in the corresponding time range.

9.  Customize a service resource report.

    a. Click **Customize** and select the service source indicators to be displayed.

       -  Service Total Disk I/O Read Speed
       -  Service Total Memory Usage
       -  Service Total Disk I/O Write Speed
       -  Service Total CPU Usage

    b. Click **OK** to save the selected monitoring metrics for display.

       .. note::

          Click **Clear** to cancel all the selected monitoring metrics in a batch.

10. Export a monitoring report.

    Click **Export**. MRS Manager will generate a report about the selected service resources in a specified time of period. Save the report.

    .. note::

       To view the curve charts of monitoring metrics in a specified period, click **View**.
