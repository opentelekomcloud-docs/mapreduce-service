:original_name: admin_guide_000038.html

.. _admin_guide_000038:

Overview
========


Overview
--------

Log in to MRS Manager, click **Cluster**, click the name of the desired cluster, and choose **Service** > **KrbServer**. On the displayed page, click **Instance**. The displayed instance management page contains the function area and role instance list.

Functional Area
---------------

After selecting the instances to be operated in the function area, you can maintain and manage the role instances, such as starting or stopping the instances. :ref:`Table 1 <admin_guide_000038__table17943743105914>` shows the main operations.

.. _admin_guide_000038__table17943743105914:

.. table:: **Table 1** Instance maintenance and management

   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UI Portal                                                     | Description                                                                                                                                                                                                                                                                                          |
   +===============================================================+======================================================================================================================================================================================================================================================================================================+
   | **Start Instance**                                            | Start a specified instance in the cluster. You can start a role instance in the **Not Started**, **Stop Failed**, or **Startup Failed** state to use the role instance.                                                                                                                              |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More > Stop Instance**                                      | Stop a specified instance in the cluster. You can stop a role instance that is no longer used or is abnormal.                                                                                                                                                                                        |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More > Restart Instance**                                   | Restart a specified instance in the cluster. You can restart an abnormal role instance to restore it.                                                                                                                                                                                                |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More > Instance Rolling Restart**                           | Restart a specified instance in the cluster without interrupting services. For details about the parameter settings, see :ref:`Performing a Rolling Restart of a Cluster <admin_guide_000012>`.                                                                                                      |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **More > Decommission/Recommission**                          | Recommission or decommission a specified instance in the cluster to change the service availability status of the service. For details, see :ref:`Decommissioning and Recommissioning an Instance <admin_guide_000040>`.                                                                             |
   |                                                               |                                                                                                                                                                                                                                                                                                      |
   |                                                               | .. note::                                                                                                                                                                                                                                                                                            |
   |                                                               |                                                                                                                                                                                                                                                                                                      |
   |                                                               |    Only the role DataNode in HDFS, role NodeManager in Yarn, and role RegionServer in HBase support the recommissioning and decommissioning functions.                                                                                                                                               |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | *Desired instance* > **More** > **Synchronize Configuration** | If the **Configuration Status** of a role instance is **Expired**, the role instance has not been restarted after the configuration is modified, and the new configuration is saved only on MRS Manager. In this case, use this function to deliver the new configuration to the specified instance. |
   |                                                               |                                                                                                                                                                                                                                                                                                      |
   |                                                               | .. note::                                                                                                                                                                                                                                                                                            |
   |                                                               |                                                                                                                                                                                                                                                                                                      |
   |                                                               |    -  After synchronizing the role instance configuration, you need to restart the role instance whose configuration has expired. The role instance is unavailable during the restart.                                                                                                               |
   |                                                               |    -  After the synchronization is complete, restart the instance for the configuration to take effect.                                                                                                                                                                                              |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | *Desired instance* > **Instance Configurations**              | For details, see :ref:`Managing Instance Configurations <admin_guide_000043>`.                                                                                                                                                                                                                       |
   +---------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

You can filter instances based on the role they belong to or their running status in the function area.

.. note::

   Click **Advanced Search** to search for specified instances by specifying other filter criteria, such as **Host Name**, **Management IP Address**, **Business IP Address**, or **Instance Groups**.

Role Instance List
------------------

The role instance list contains the instances of all roles in the cluster. The list displays the running status, configuration status, hosts, and related IP addresses of each instance.

.. table:: **Table 2** Instance running status

   +---------------------+----------------------------------------------------------------------------------------------------------+
   | Status              | Description                                                                                              |
   +=====================+==========================================================================================================+
   | **Normal**          | Indicates that the instance is running properly.                                                         |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Faulty**          | Indicates that the instance cannot run properly.                                                         |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Decommissioned**  | Indicates that the instance is out of service.                                                           |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Not started**     | Indicates that the instance is stopped.                                                                  |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Unknown**         | Indicates that the initial status of the instance cannot be detected.                                    |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Starting**        | Indicates that the instance is being started.                                                            |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Stopping**        | Indicates that the instance is being stopped.                                                            |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Restoring**       | Indicates that an exception may occur in the instance and the instance is being automatically rectified. |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Decommissioning** | Indicates that the instance is being decommissioned.                                                     |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Recommissioning** | Indicates that the instance is being recommissioned.                                                     |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Failed to start** | Indicates that the service fails to be started.                                                          |
   +---------------------+----------------------------------------------------------------------------------------------------------+
   | **Failed to stop**  | Indicates that the service fails to be stopped.                                                          |
   +---------------------+----------------------------------------------------------------------------------------------------------+

Instance Details
----------------

You can click an instance name to go to the instance details page and view the basic information, configuration file, instance logs, and monitoring metric reports of the instance.
