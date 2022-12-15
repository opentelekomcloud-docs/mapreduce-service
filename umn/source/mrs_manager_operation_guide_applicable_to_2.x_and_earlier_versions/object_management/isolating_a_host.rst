:original_name: mrs_01_0255.html

.. _mrs_01_0255:

Isolating a Host
================

Scenario
--------

If a host is found to be abnormal or faulty, affecting cluster performance or preventing services from being provided, you can temporarily exclude that host from the available nodes in the cluster. In this way, the client can access other available nodes. In scenarios where patches are to be installed in a cluster, you can also exclude a specified node from patch installation.

Users can isolate a host manually on MRS Manager based on the actual service requirements or O&M plan. Only non-management nodes can be isolated.

Impact on the System
--------------------

-  After a host is isolated, all role instances on the host will be stopped. You cannot start, stop, or configure the host and any instances on the host.
-  After a host is isolated, statistics about the monitoring status and indicator data of the host hardware and instances on the host cannot be collected or displayed.

Procedure
---------

#. On MRS Manager, click **Hosts**.

#. Select the check box of the host to be isolated.

#. Choose **More** > **Isolate Host**,

#. and click **OK** in the displayed dialog box.

   After **Operation successful.** is displayed, click **Finish**. The host is isolated successfully, and the value of **Operating Status** becomes **Isolated**.

   .. note::

      For isolated hosts, you can cancel the isolation and add them to the cluster again. For details, see :ref:`Canceling Host Isolation <mrs_01_0256>`.
