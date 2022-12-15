:original_name: mrs_08_0027.html

.. _mrs_08_0027:

Constraints
===========

Before using MRS, ensure that you have read and understand the following restrictions.

-  MRS clusters must be created in VPC subnets.
-  You are advised to use any of the following browsers to access MRS:

   -  Google Chrome: 36.0 or later

   -  Internet Explorer: 9.0 or later

      If you use Internet Explorer 9.0, you may fail to log in to the MRS management console because user **Administrator** is disabled by default in some Windows systems, such as Windows 7 Ultimate. Internet Explorer automatically selects a system user for installation. As a result, Internet Explorer cannot access the management console. Reinstall Internet Explorer 9.0 or later (recommended) or run Internet Explorer 9.0 as user **Administrator**.

-  When you create an MRS cluster, you can select **Auto create** from the drop-down list of **Security Group** to create a security group or select an existing security group. After the MRS cluster is created, do not delete or modify the used security group. Otherwise, a cluster exception may occur.
-  To prevent illegal access, only assign access permission for security groups used by MRS where necessary.
-  Do not perform the following operations because they will cause cluster exceptions:

   -  Shutting down, restarting, or deleting MRS cluster nodes displayed in ECS, changing or reinstalling their OS, or modifying their specifications.
   -  Deleting the existing processes, applications or files on cluster nodes.

-  If a cluster exception occurs when no incorrect operations have been performed, contact technical support engineers. They will ask you for your key and then perform troubleshooting.
-  Plan disks of cluster nodes based on service requirements. If you want to store a large volume of service data, add EVS disks or storage space to prevent insufficient storage space from affecting node running.
-  The cluster nodes store only users' service data. Non-service data can be stored in the OBS or other ECS nodes.
-  The cluster nodes only run MRS cluster programs. Other client applications or user service programs are deployed on separate ECS nodes.
-  When you expand the storage capacity of nodes (including master, core, and task) in an MRS cluster, you are advised to create new disks and then attach them to the nodes.
-  The capacity (including storage and computing capabilities) of an MRS cluster can be expanded by adding core or task nodes.
-  If the cluster is still used to execute tasks or modify configurations after a master node in the cluster is stopped, and other master nodes in the cluster are stopped before the stopped master node is started after task execution or configuration modification, data may be lost due to an active/standby switchover. In this scenario, after the task is executed or the configuration is modified, start the master node that has been stopped and then stop all nodes. If all nodes in the cluster have been stopped, start them in the reverse order of node shutdown.
-  The Capacity and Superior scheduler switchover is complete when the MRS cluster is used, while configuration synchronization is not complete. Configure synchronization again based on the new scheduler if necessary.
