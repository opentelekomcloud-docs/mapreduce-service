:original_name: mrs_01_0383.html

.. _mrs_01_0383:

Managing Storm Topologies
=========================

Scenario
--------

You can manage Storm topologies on the Storm web UI. Users in the **storm** group can manage only the topology tasks submitted by themselves, while users in the **stormadmin** group can manage all topology tasks.

Procedure
---------

#. For details about how to access the Storm WebUI, see :ref:`Accessing the Storm Web UI <mrs_01_0382>`.

#. In the **Topology summary** area, click the desired topology.

#. Use options in **Topology actions** to manage the Storm topology.

   -  Activating a topology

      Click **Activate** to activate the topology.

   -  Deactivating a topology

      Click **Deactivate** to deactivate the topology.

   -  Re-deploying a topology

      Click **Rebalance** and specify the wait time (in seconds) of re-deployment. Generally, if the number of nodes in a cluster changes, the topology can be re-deployed to maximize resource usage.

   -  Deleting a topology

      Click **Kill** and specify the wait time (in seconds) of the deletion.

   -  Starting or stopping sampling messages

      Click **Debug**. In the dialog box displayed, specify the percentage of the sampled data volume. For example, if the value is set to **10**, 10% of data is sampled.

      To stop sampling, click **Stop Debug**.

      .. note::

         This function is available only if the sampling function is enabled when the topology is submitted. For details about querying data processing information, see :ref:`Querying Storm Topology Logs <mrs_01_0384>`.

   -  Modifying the topology log level

      Click **Change Log Level** to specify a new log level.

#. Displaying a topology

   In the **Topology Visualization** area, click **Show Visualization** to visualize the topology.
