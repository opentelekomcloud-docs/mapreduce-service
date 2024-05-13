:original_name: mrs_01_0101.html

.. _mrs_01_0101:

Introduction to MRS Manager
===========================

Overview
--------

MRS manages and analyzes massive data and helps you rapidly obtain desired data from structured and unstructured data. The structure of open-source components is complex. The installation, configuration, and management processes are time- and labor-consuming. MRS Manager is a unified enterprise-level cluster management platform and provides the following functions:

-  Cluster monitoring enables you to quickly view the health status of hosts and services.
-  Graphical metric monitoring and customization enable you to quickly obtain key information about the system.
-  Service property configurations can meet service performance requirements.
-  With cluster, service, and role instance functions, you can start or stop services and clusters in one click.

Introduction to the MRS Manager GUI
-----------------------------------

MRS Manager provides a unified cluster management platform, facilitating rapid and easy O&M for clusters. For details about how to access MRS Manager, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.

:ref:`Table 1 <mrs_01_0101__en-us_topic_0035209593_table13549662121428>` describes the functions of each operation entry.

.. _mrs_01_0101__en-us_topic_0035209593_table13549662121428:

.. table:: **Table 1** Functions of each entry on the operation bar

   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Function                                                                                                                                                                                                                                                                                                                         |
   +===========+==================================================================================================================================================================================================================================================================================================================================+
   | Dashboard | Displays the status of all services, main monitoring indicators of each service, and host status in charts, such as bar charts, line charts, and tables. You can customize a dashboard for the key monitoring indicators and drag it to any position on the interface. The system dashboard page supports automatic data update. |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Services  | Provides the service monitoring, operation, and configuration guidance, which helps you manage services in a unified manner.                                                                                                                                                                                                     |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Hosts     | Provides guidance on how to monitor, operate, and configure hosts, helping you manage hosts in a unified manner.                                                                                                                                                                                                                 |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Alarms    | Supports alarm query and provides guidance on alarm handling, helping you identify and rectify product faults and potential risks in a timely manner to ensure normal system operation.                                                                                                                                          |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit     | Allows authorized users to query and export audit logs, helping you to view all user activities and operations.                                                                                                                                                                                                                  |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tenant    | Provides a unified tenant management platform.                                                                                                                                                                                                                                                                                   |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | System    | Provides monitoring, alarm configuration management, and backup management.                                                                                                                                                                                                                                                      |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Go to the **System** tab page, and switch to another function pages through shortcuts. See :ref:`Table 2 <mrs_01_0101__en-us_topic_0035209593_table5212148312126>`.

The following is an example of quick redirection through shortcuts:

#. On MRS Manager, click **System**.

#. On the **System** tab page, click a function link. The function page is displayed.

   For example, in the **Backup and Restoration** area, click **Back Up Data**. The page for backing up data is displayed.

#. Move the cursor to the left border of the browser window. The **System** black shortcut menu is displayed. After you move the cursor out of the menu, the menu is collapsed.

#. In the shortcut menu that is displayed, you can click a function link to go to the corresponding function page.

   For example, choose **Maintenance > Export Log**. The page for exporting logs is displayed.

.. _mrs_01_0101__en-us_topic_0035209593_table5212148312126:

.. table:: **Table 2** Shortcut menus on the **System** tab page

   ====================== =======================================
   Menu                   Function Link
   ====================== =======================================
   Backup and Restoration Back Up Data
   \                      Restore Data
   Maintenance            Export Log
   \                      Export Audit Log
   \                      Check Health Status
   Monitoring and Alarm   Configure Syslog
   \                      Configure Alarm Threshold
   \                      Configure SNMP
   \                      Configure Monitoring Metric Dump
   \                      Configure Resource Contribution Ranking
   Permission             Manage User
   \                      Manage User Group
   \                      Manage Role
   \                      Configure Password Policy
   \                      Change OMS Database Password
   Patch                  Manage Patch
   ====================== =======================================

Reference
---------

MapReduce Service (MRS) is a data analysis service on the public cloud. It is used to manage and analyze massive sets of data.

MRS uses MRS Manager to manage big data components, such as components in the Hadoop ecosystem. Therefore, some concepts on the MRS Console on the public cloud must be different from those on MRS Manager. For details, see :ref:`Table 3 <mrs_01_0101__en-us_topic_0035209593_table39303837105524>`.

.. _mrs_01_0101__en-us_topic_0035209593_table39303837105524:

.. table:: **Table 3** Difference Comparison

   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | Concept           | Public Cloud MRS                                                                                                                                            | MRS Manager                                                                        |
   +===================+=============================================================================================================================================================+====================================================================================+
   | MapReduce Service | Indicates the data analysis cloud service on the public cloud, called MRS. This service includes components such as Hive, Spark, Yarn, HDFS, and ZooKeeper. | Provides a unified management platform for big data components in tenant clusters. |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
