:original_name: mrs_01_0086.html

.. _mrs_01_0086:

Determining Active and Standby Management Nodes of Manager
==========================================================

This section describes how to determine the active and standby management nodes of Manager on the Master1 node.

Background
----------

You can log in to other nodes in the cluster from the Master node. After logging in to the Master node, you can determine the active and standby management nodes of Manager and run commands on corresponding management nodes.

In active/standby mode, a switchover can be implemented between Master1 and Master2. For this reason, Master1 may not be the active management node for Manager.

Procedure
---------

#. Confirm the Master nodes of an MRS cluster.

   a. In the navigation tree of the MRS management console, choose **Clusters > Active Clusters**, select a running cluster, and click its name to switch to the cluster details page. View basic information of the specified cluster.
   b. On the **Nodes** tab page, view the node name. The node that contains **master1** in its name is the Master1 node. The node that contains **master2** in its name is the Master2 node.

#. Determine the active and standby Manager management nodes.

   a. Remotely log in to the Master1 node. For details, see :ref:`Logging In to an ECS <mrs_01_0083>`.

   b. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   c. Run the following command to identify the active and standby management nodes:

      For versions earlier than MRS 3.\ *x*, run the **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh** command.

      For MRS 3.\ *x* or later: Run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command.

      In the command output, the node whose **HAActive** is **active** is the active management node (mgtomsdat-sh-3-01-1 in the following example), and the node whose **HAActive** is **standby** is the standby management node (mgtomsdat-sh-3-01-2 in the following example).

      .. code-block::

         Ha mode
         double
         NodeName              HostName                      HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
         192-168-0-30          mgtomsdat-sh-3-01-1           V100R001C01        2014-11-18 23:43:02      active               normal               Actived
         192-168-0-24          mgtomsdat-sh-3-01-2           V100R001C01        2014-11-21 07:14:02      standby              normal               Deactived

      .. note::

         If the Master1 node to which you have logged in is the standby management node and you need to log in to the active management node, run the following command:

         **ssh** *IP address of Master2 node*
