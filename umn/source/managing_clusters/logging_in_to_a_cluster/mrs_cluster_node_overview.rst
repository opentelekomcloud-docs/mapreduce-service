:original_name: mrs_01_0081.html

.. _mrs_01_0081:

MRS Cluster Node Overview
=========================

This section describes remote login, MRS cluster node types, and node functions.

MRS cluster nodes support remote login. The following remote login methods are available:

-  GUI login: Use the remote login function provided by the ECS management console to log in to the Linux interface of the Master node in the cluster. For details, see :ref:`Logging In to an ECS <mrs_01_0083>`.

-  SSH login: Applies to Linux ECSs only. You can use a remote login tool (such as PuTTY) to log in to an ECS. The ECS must have a bound EIP.

   For details about how to apply for and bind EIP for the Master node, see **Virtual Private Cloud** > **User Guide** > **Elastic IP** > **Assigning an EIP and Binding It to an ECS**.

   You can log in to a Linux ECS using either a key pair or password.

   .. important::

      If you use a key pair to access a node in a cluster of MRS 1.6.2 earlier, you need to log in to the node as a Linux user. For details, see :ref:`Logging In to an ECS Using a Key Pair (SSH) <mrs_01_0083__section5513107114>`.

      If you use a key pair to access a node in a cluster of MRS 1.6.2 or later, you need to log in to the node as user **root**. For details, see :ref:`Logging In to an ECS Using a Key Pair (SSH) <mrs_01_0083__section5513107114>`.

In an MRS cluster, a node is an ECS. :ref:`Table 1 <mrs_01_0081__table1615555733016>` describes the node types and node functions.

.. _mrs_01_0081__table1615555733016:

.. table:: **Table 1** Cluster node types

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Node Type                         | Functions                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   +===================================+====================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Master node                       | Management node of an MRS cluster. It manages and monitors the cluster. In the navigation tree of the MRS management console, choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page. On the **Nodes** tab page, view the **Name**. The node that contains **master1** in its name is the Master1 node. The node that contains **master2** in its name is the Master2 node. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                                   | You can log in to a Master node either using VNC on the ECS management console or using SSH. After logging in to the Master node, you can access Core nodes without entering passwords.                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                                   | The system automatically deploys the Master nodes in active/standby mode and supports the high availability (HA) feature for MRS cluster management. If the active management node fails, the standby management node switches to the active state and takes over services.                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                                   | To determine whether the Master1 node is the active management node, see :ref:`Determining Active and Standby Management Nodes of Manager <mrs_01_0086>`.                                                                                                                                                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Core node                         | Work node of an MRS cluster. It processes and analyzes data and stores process data.                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Task node                         | Compute node. It is used for auto scaling when the computing resources in a cluster are insufficient.                                                                                                                                                                                                                                                                                                                                              |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
