:original_name: admin_guide_000051.html

.. _admin_guide_000051:

Viewing the Host List
=====================

Overview
--------

Log in to FusionInsight Manager, click **Hosts**, and the host list is displayed on the host management page. You can view the host list and basic information of each host.

You can switch view types and set search criteria to filter and search for hosts.

Host View
---------

You can click **Role View** to view the roles deployed on each host. If the role supports the active/standby mode, the role name is displayed in bold.

Host List
---------

The host list on the host management page contains all hosts in the cluster, and O&M operations can be performed on these hosts.

On the host management page, you can filter hosts by node type or cluster. The rules for filtering host types are as follows:

-  A management node is the node where OMS is deployed. Additionally, control roles and data roles may also be deployed on management nodes.
-  A control node is the node where control roles are deployed. Additionally, data roles may also be deployed on control nodes.
-  A Data Node is the node where only data roles are deployed.

If you select the **Host View**, the IP address, rack planning, AZ name, running status, cluster name, and hardware resource usage of each host are displayed.

.. table:: **Table 1** Host running status

   +---------------+-------------------------------------------------------------------+
   | Status        | Description                                                       |
   +===============+===================================================================+
   | **Normal**    | Indicates that the host is in the normal state.                   |
   +---------------+-------------------------------------------------------------------+
   | **Faulty**    | Indicates that the host is abnormal.                              |
   +---------------+-------------------------------------------------------------------+
   | **Unknown**   | Indicates that the initial status of the host cannot be detected. |
   +---------------+-------------------------------------------------------------------+
   | **Isolated**  | Indicates that the host is isolated.                              |
   +---------------+-------------------------------------------------------------------+
   | **Suspended** | Indicates that the host is stopped.                               |
   +---------------+-------------------------------------------------------------------+
