:original_name: admin_guide_000030.html

.. _admin_guide_000030:

Service Details Page
====================

Overview
--------

Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services**. In the service list, click the specified service name to go to the service details page, including the **Dashboard**, **Instance**, **Instance Groups** and **Configurations** tab pages as well as function areas. For some services, the custom management tool page can be displayed.For details about the supported management tools, see :ref:`Table 1 <admin_guide_000030__table1936171313284>`..

.. _admin_guide_000030__table1936171313284:

.. table:: **Table 1** Customized management tools

   +------------------------------+---------+-------------------------------------------------------------------+
   | Tool                         | Service | Description                                                       |
   +==============================+=========+===================================================================+
   | Flume configuration tool     | Flume   | Configures collection parameters for the Flume server and client. |
   +------------------------------+---------+-------------------------------------------------------------------+
   | Flume client management tool | Flume   | Views the monitoring information about the Flume client.          |
   +------------------------------+---------+-------------------------------------------------------------------+
   | Kafka topic monitoring tool  | Kafka   | Monitors and manages Kafka topics.                                |
   +------------------------------+---------+-------------------------------------------------------------------+

The **Dashboard** page is the default page, which contains the basic information, role list, dependency table, and monitoring chart, and more. You can manage services in the upper right corner. For details about basic service management, such as starting, stopping, rolling restart, and synchronization configuration, see :ref:`Table 3 <admin_guide_000027__table17943743105914>`. For details about other service management operations, see :ref:`Table 2 <admin_guide_000030__table15518145510269>`.

.. _admin_guide_000030__table15518145510269:

.. table:: **Table 2** Service management operations

   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Navigation Path                            | Description                                                                                                                                                                                                                                                                |
   +============================================+============================================================================================================================================================================================================================================================================+
   | **More** > **Health Check**                | Performs a health check for the current service. The health check items include the health status of each check object, related alarms, and user-defined monitoring indicators. The check result is not the same as the values of **Running Status** displayed on the GUI. |
   |                                            |                                                                                                                                                                                                                                                                            |
   |                                            | To export the result of the health check, click **Export Report** in the upper left corner of the checklist. If you find any problem, click **View Help**.                                                                                                                 |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More** > **Download Client**             | Download the default client that contains only specific services and perform management operations, run services, or perform secondary development on the client. For details, see :ref:`Downloading the Client <admin_guide_000014>`.                                     |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More** > **Change Service Name**         | Changes the name of the current service.                                                                                                                                                                                                                                   |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More** > **Perform** *XX* **Switchover** | For details, see :ref:`Performing Active/Standby Switchover of a Role Instance <admin_guide_000031>`.                                                                                                                                                                      |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More** > **Enter/Exit Maintenance Mode** | Configures a service to enter/exit the maintenance mode.                                                                                                                                                                                                                   |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Configurations** > **Import/Export**     | In the scenario where services are migrated to a new cluster or the same services are deployed again, you can import or export all configuration data of a specific service to quickly copy the configuration results.                                                     |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Basic Information Area
----------------------

The basic information area on the **Dashboard** tab page contains the basic status data of the service, including the running status, configuration details, version, and key information of the service. If the service supports the open-source web UIs, you can access the open-source web UIs by clicking the links in the basic information area.

.. note::

   In the current version, user **admin** does not have the permission to access all the service functions provided on the open source web UI. Create a component service administrator to access the WebUI address.

Role List
---------

The role list on the **Dashboard** tab page contains all roles of the service. The role list displays the running status and the number of instances of each role.

Dependency
----------

The dependency relationship table on the **Dashboard** tab page displays the services on which the current service depends and other services that depend on the service.

Historical Records of Alarms and Events
---------------------------------------

The alarm and event history area displays the key alarms and events reported by the current service. Up to 20 historical records are displayed.

Chart
-----

The chart area is displayed on the right of the **Dashboard** tab page and contains the key monitoring indicator report of the service. You can customize the monitoring report that is displayed in the chart area, view the description of the monitoring metrics, or export the monitoring data. For a customized resource contribution chart, you can zoom in on the chart and switch between the trend chart and distribution chart.

.. note::

   Some services in the cluster provide service-level resource monitoring items. For details, see :ref:`Resource Monitoring <admin_guide_000032>`.
