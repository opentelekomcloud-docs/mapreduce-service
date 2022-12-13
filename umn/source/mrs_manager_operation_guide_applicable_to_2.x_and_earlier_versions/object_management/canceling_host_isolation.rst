:original_name: mrs_01_0256.html

.. _mrs_01_0256:

Canceling Host Isolation
========================

Scenario
--------

After the exception or fault of a host is handled, you must cancel the isolation of the host for proper usage.

Users can cancel the isolation of a host on MRS Manager.

Prerequisites
-------------

-  The host is in the **Isolated** state.
-  The exception or fault of the host has been rectified.

Procedure
---------

#. On MRS Manager, click **Hosts**.

#. Select the check box of the host to be de-isolated.

#. Choose **More** > **Cancel Host Isolation**,

#. and click **OK** in the displayed dialog box.

   After **Operation successful.** is displayed, click **Finish**. The host is de-isolated successfully, and the value of **Operating Status** becomes **Normal**.

#. Click the name of the de-isolated host to show its status, and click **Start All Roles**.
