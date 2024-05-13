:original_name: admin_guide_000082.html

.. _admin_guide_000082:

Creating a Backup Restoration Task
==================================

Scenario
--------

You can create a backup restoration task on MRS Manager. After the restoration task is executed, the specified backup data is restored to the cluster.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **O&M** > **Backup and Restoration** > **Restoration Management**. On the page that is displayed, click **Create**.

#. Configure **Task Name**.

#. Set **Recovery Object** to **OMS** or the cluster whose data you want to restore.

#. Set the required parameters in the **Recovery Configuration** area.

   -  Metadata and service data can be restored.
   -  For details about how to restore data of different components, see :ref:`Backup and Recovery Management <admin_guide_000198>`.

#. Click **OK** to save the configurations.

#. In the restoration task list, you can view the created restoration tasks.

   Locate the row containing the target restoration task, click **Start** in the **Operation** column to execute the restoration task immediately.
