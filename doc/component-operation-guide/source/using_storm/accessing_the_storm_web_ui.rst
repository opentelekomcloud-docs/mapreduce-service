:original_name: mrs_01_0382.html

.. _mrs_01_0382:

Accessing the Storm Web UI
==========================

Scenario
--------

The Storm web UI provides a graphical interface for using Storm.

The following information can be queried on the Storm web UI:

-  Storm cluster summary
-  Nimbus summary
-  Topology summary
-  Supervisor summary
-  Nimbus configurations

Prerequisites
-------------

-  The password of user **admin** has been obtained. The password of user **admin** is specified by you during the cluster creation.
-  If a user other than **admin** is used to access the Storm web UI, the user must be added to the **storm** or **stormadmin** user group.

Procedure
---------

#. Access the component management page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
   -  For versions earlier than MRS 3.\ *x*, click the cluster name to go to the cluster details page and choose **Components**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Log in to the Storm WebUI.

   -  For versions earlier than MRS 3.x: Choose **Storm**. On the **Storm Summary** area, click any UI link on the right side of **Storm Web UI** to open the Storm web UI.

      .. note::

         When accessing the Storm web UI for the first time, you must add the address to the trusted site list.

   -  For MRS 3.x or later, choose **Storm** > **Overview**. In the **Basic Information** area, click any UI link on the right side of **Storm Web UI** to open the Storm web UI.

Related Tasks
-------------

-  Click a topology name to view details, status, Spouts information, Bolts information, and configuration information of the topology.
-  In the **Topology actions** area, click **Activate**, **Deactivate**, **Rebalance**, **Kill**, **Debug**, **Stop Debug**, and **Change Log Level** to activate, deactivate, redeploy, delete, debug, and stop debugging the topology, and modify the log levels, respectively. You need to set the waiting time for the redeployment and deletion operations. The unit is second.
-  In the **Topology Visualization** area, click **Show Visualization** to visualize a topology. After the topology is visualized, the WebUI displays the topology structure.
