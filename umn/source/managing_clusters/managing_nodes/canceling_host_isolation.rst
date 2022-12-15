:original_name: mrs_01_0213.html

.. _mrs_01_0213:

Canceling Host Isolation
========================

Scenario
--------

After the exception or fault of a host is handled, you must cancel the isolation of the host for proper usage.

You can cancel the isolation of a host on MRS.

Prerequisites
-------------

-  The host is in the **Isolated** state.
-  The exception or fault of the host has been rectified.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Nodes**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Canceling Host Isolation <mrs_01_0256>`.

#. Unfold the node group information and select the check box of the target host that you want to cancel its isolation.

#. Choose **Node Operation** > **Cancel Host Isolation**.

#. Confirm the information about the host for which the isolation is to be cancelled and click **OK**.

   When **Operation successful** is displayed, click **Finish**. The host is de-isolated successfully, and the value of **Operating Status** becomes **Normal**.

#. Select the host that has been de-isolated and choose **Node Operation** > **Start All Roles**.
