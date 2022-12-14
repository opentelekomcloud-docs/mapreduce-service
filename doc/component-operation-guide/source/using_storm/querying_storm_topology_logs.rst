:original_name: mrs_01_0384.html

.. _mrs_01_0384:

Querying Storm Topology Logs
============================

Scenario
--------

You can query topology logs to check the execution of a Storm topology in a worker process. To query the data processing logs of a topology, enable the **Debug** function when submitting the topology. Only streaming clusters with Kerberos authentication enabled support this function. In addition, the user who queries topology logs must be the one who submits the topology or a member of the **stormadmin** group.

Prerequisites
-------------

-  The network of the working environment has been configured.
-  The sampling function has been enabled for the topology.

Querying Worker Process Logs
----------------------------

#. For details about how to access the Storm WebUI, see :ref:`Accessing the Storm Web UI <mrs_01_0382>`.
#. In the **Topology Summary** area, click the desired topology to view details.
#. Click the desired **Spouts** or **Bolts** task. In the **Executors (All time)** area, click a port in **Port** to view detailed logs.

Querying Data Processing Logs of a Topology
-------------------------------------------

#. For details about how to access the Storm WebUI, see :ref:`Accessing the Storm Web UI <mrs_01_0382>`.
#. In the **Topology Summary** area, click the desired topology to view details.
#. Click **Debug**, specify the data sampling ratio, and click **OK**.
#. Click the **Spouts** or **Bolts** task. In **Component summary**, click **events** to view data processing logs.
