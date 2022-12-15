:original_name: mrs_01_0211.html

.. _mrs_01_0211:

Managing a Host (Node)
======================

Scenario
--------

To check an abnormal or faulty host (node), you need to stop all host roles on MRS. To recover host services after the host fault is rectified, restart all roles.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Nodes**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Managing a Host <mrs_01_0254>`.

#. Unfold the node group information and select the check box of the target node.
#. Choose **Node Operation** > **Start All Roles** or **Stop All Roles** to perform the required operation.
