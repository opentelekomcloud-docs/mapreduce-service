:original_name: mrs_01_0212.html

.. _mrs_01_0212:

Isolating a Host
================

Scenario
--------

If a host is found to be abnormal or faulty, affecting cluster performance or preventing services from being provided, you can temporarily exclude that host from the available nodes in the cluster. In this way, the client can access other available nodes. In scenarios where patches are to be installed in a cluster, you can also exclude a specified node from patch installation.

You can isolate a host manually on MRS based on the actual service requirements or O&M plan. Only non-management nodes can be isolated.

Impact on the System
--------------------

-  After a host is isolated, all role instances on the host will be stopped. You cannot start, stop, or configure the host and any instances on the host.
-  After a host is isolated, statistics of the monitoring status and indicator data of the host hardware and instances cannot be collected or displayed.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Nodes**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Isolating a Host <mrs_01_0255>`.

#. Unfold the node group information and select the check box of the target host.

#. Choose **Node Operation** > **Isolate Host**.

#. Confirm the information about the host to be isolated and click **OK**.

   When **Operation successful** is displayed, click **Finish**. The host is isolated successfully, and the value of **Operating Status** becomes **Isolated**.

   .. note::

      For isolated hosts, you can cancel the isolation and add them to the cluster again. For details, see :ref:`Canceling Host Isolation <mrs_01_0213>`.
