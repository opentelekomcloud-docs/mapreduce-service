:original_name: mrs_01_0041.html

.. _mrs_01_0041:

Manually Scaling Out a Cluster
==============================

The storage and computing capabilities of MRS can be improved by simply adding Core nodes or Task nodes instead of modifying system architecture, reducing O&M costs. Core nodes can process and store data. You can add Core nodes to expand the node quantities and handle peak loads. Task nodes are used for computing and do not store persistent data.

Background
----------

The MRS cluster supports a maximum of 500 Core and Task nodes. If more than 500 Core/Task nodes are required, contact technical support engineers or invoke a background interface to modify the database.

Core nodes and Task nodes can be added, excluding the Master node. Here, the maximum number of Core/Task nodes to be added is 500 minus the number of Core/Task nodes. For example, the current number of Core nodes is 3, the number of Core nodes to be added must be less than or equal to 497. If the cluster scale-out fails, you can add node to the cluster again.

If no node is added during cluster creation, you can specify the number of nodes to be added during scale-out. However, you cannot specify the nodes to be added.

The operations for scaling out a cluster vary depending on the selected version.

Procedure
---------

#. Log in to the MRS console.

#. Click |image1| in the upper-left corner on the management console and select a region and project.

#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.

#. Click the **Nodes** tab. In the **Operation** column of the node group, click **Scale Out**. The **Scale Out** page is displayed.

   The scale-out operation can only be performed on the running clusters.

#. Set **Scaled Out Nodes** and **Run Bootstrap Action**, and click **OK**

   .. note::

      -  If the Task node group does not exist in the cluster, configure the Task node by referring to :ref:`Adding a Task Node <mrs_01_0041__section1077318341361>`.
      -  If a bootstrap action is added during cluster creation, the **Run Bootstrap Action** parameter is valid. If this function is enabled, the bootstrap actions added during cluster creation will be run on all the scaled out nodes.
      -  If the **New Specifications** parameter is available, the specifications that are the same as those of the original nodes have been sold out or discontinued. Nodes with new specifications will be added.
      -  Before scaling out the cluster, check whether its security group configuration is correct. Ensure that an inbound security group rule contains a rule in which **Protocol & Port** is set to **All**, and **Source** is set to a trusted accessible IP address range.

#. In the **Scale Out Node** dialog box, click **OK**.

#. A dialog box is displayed, indicating that the scale-out task is submitted successfully.

   The following parameters explain the cluster scale-out process:

   -  Expanding: If a cluster is being expanded, its status is **Scaling out**. The submitted jobs will be executed and you can submit new jobs. You are not allowed to continue to scale out, or delete the cluster. You are advised not to restart the cluster or modify the cluster configuration.
   -  Expansion succeeded: If a cluster is expanded successfully, its status is **Running**.
   -  Failed scale-out: The cluster status is **Running** when the cluster scale-out failed. You can execute jobs and scale out the cluster again.

   After the cluster is scaled out, you can view the node information of the cluster on the **Nodes** page.

.. _mrs_01_0041__section1077318341361:

Adding a Task Node
------------------

To add a task node to a custom cluster, perform the following steps:

#. On the cluster details page, click the **Nodes** tab and click **Add Node Group**. The **Add Node Group** page is displayed.
#. Select **NM** for **Deploy Roles** and set other parameters as required.

To add a task node to a non-custom cluster, perform the following steps:

#. On the cluster details page, click the **Nodes** tab and click **Configure Task Node**. The **Configure Task Node** page is displayed.
#. On the **Configure Task Node** page, set **Node Type**, **Instance Specifications**, **Nodes**, **System Disk**. In addition, if **Add Data Disk** is enabled, configure the storage type, size, and number of data disks.
#. Click **OK**.

.. _mrs_01_0041__section8614439391:

Adding a Node Group
-------------------

.. note::

   Used to add node groups and applies to customized clusters of MRS 3.\ *x*.

#. On the cluster details page, click the **Nodes** tab and click **Add Node Group**. The **Add Node Group** page is displayed.
#. Set the parameters as needed.

   .. table:: **Table 1** Parameters for adding a node group

      +-------------------------+------------------------------------------------------------------------------------------------+
      | Parameter               | Description                                                                                    |
      +=========================+================================================================================================+
      | Instance Specifications | Select the flavor type of the hosts in the node group.                                         |
      +-------------------------+------------------------------------------------------------------------------------------------+
      | Nodes                   | Set the number of nodes in the node group.                                                     |
      +-------------------------+------------------------------------------------------------------------------------------------+
      | System Disk             | Set the specifications and capacity of the system disk on the new node.                        |
      +-------------------------+------------------------------------------------------------------------------------------------+
      | Data Disk (GB)          | Set the specifications, capacity, and number of data disks of the new node.                    |
      +-------------------------+------------------------------------------------------------------------------------------------+
      | Deploy Roles            | Deploy the instances of each node in the new node group. The setting can be manually adjusted. |
      +-------------------------+------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349257269.png
