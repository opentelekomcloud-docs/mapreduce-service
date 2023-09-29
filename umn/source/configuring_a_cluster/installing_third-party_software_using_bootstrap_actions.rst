:original_name: mrs_01_0413.html

.. _mrs_01_0413:

Installing Third-Party Software Using Bootstrap Actions
=======================================================

This operation applies to clusters earlier than MRS 3.x.

Prerequisites
-------------

The bootstrap action script has been prepared by referring to :ref:`Preparing the Bootstrap Action Script <mrs_01_0417>`.

Adding a Bootstrap Action When Creating a Cluster
-------------------------------------------------

#. Log in to the MRS management console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. Click the **Custom Config** tab.

#. Configure the cluster software and hardware by referring to :ref:`Creating a Custom Cluster <mrs_01_0513>`.

#. On the **Set Advanced Options** tab page, click **Add** in the **Bootstrap Action** area.

   .. table:: **Table 1** Parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================+
      | Name                              | Name of a bootstrap action script                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                    |
      |                                   | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and must not start with a space.                                                                              |
      |                                   |                                                                                                                                                                                                    |
      |                                   | The value can contain 1 to 64 characters.                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                    |
      |                                   |    A name must be unique in the same cluster. You can set the same name for different clusters.                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Script Path                       | Script path. The value can be an OBS file system path or a local VM path.                                                                                                                          |
      |                                   |                                                                                                                                                                                                    |
      |                                   | -  An OBS file system path must start with **s3a://** and end with **.sh**, for example, **s3a://mrs-samples/**\ *xxx*\ **.sh**.                                                                   |
      |                                   | -  A local VM path must start with a slash (/) and end with **.sh**.                                                                                                                               |
      |                                   |                                                                                                                                                                                                    |
      |                                   |    .. note::                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                    |
      |                                   |       A path must be unique in the same cluster, but can be the same for different clusters.                                                                                                       |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Bootstrap action script parameters                                                                                                                                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Execution Node                    | Select a type of the node where the bootstrap action script is executed.                                                                                                                           |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Executed                          | Select the time when the bootstrap action script is executed.                                                                                                                                      |
      |                                   |                                                                                                                                                                                                    |
      |                                   | -  Before initial component start                                                                                                                                                                  |
      |                                   | -  After initial component start                                                                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Action upon Failure               | Whether to continue to execute subsequent scripts and create a cluster after the script fails to be executed.                                                                                      |
      |                                   |                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                    |
      |                                   |    You are advised to set this parameter to **Continue** in the debugging phase so that the cluster can continue to be installed and started no matter whether the bootstrap action is successful. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   After the bootstrap action is added, you can edit, clone, or delete it in the **Operation** column.

Adding an Automation Script on the Auto Scaling Page
----------------------------------------------------

#. Log in to the MRS management console.

#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to go to its details page.

#. Click the **Nodes** tab. On this tab page, click **Auto Scaling** in the **Operation** column of the task node group. The **Auto Scaling** page is displayed.

   If no task nodes are available, click **Configure Task Node** to add a task node and then perform this step.

   .. note::

      **Configure Task Node** is available only for MRS 3.\ *x* or later analysis, streaming, and hybrid clusters.

#. Configure a resource plan.

   Configuration procedure:

   a. On the **Auto Scaling** page, enable **Auto Scaling**.

   b. For example, the **Default Range** of node quantity is set to **2-2**, indicating that the number of task nodes is fixed to 2 except the time range specified in the resource plan.

   c. Click **Configure Node Range for Specific Time Range** under **Default Range**.

   d. Configure **Time Range** and **Node Range**. For example, set **Time Range** to **07:00-13:00**, and **Node Range** to **5-5**. This indicates that the number of task nodes is fixed to 5 in the time range specified in the resource plan. For details about the parameters, see :ref:`Table 3 <mrs_01_0061__table1846575414619>`.

      You can click **Configure Node Range for Specific Time Range** to configure multiple resource plans.

#. (Optional) Configure automation scripts.

   a. Set **Advanced Settings** to **Configure**.
   b. Click **Create**. The **Automation Script** page is displayed.

   c. Set **Name**, **Script Path**, **Execution Node**, **Parameter**, **Executed**, and **Action upon Failure**. For details about the parameters, see :ref:`Table 4 <mrs_01_0061__table15644113520578>`.
   d. Click **OK** to save the automation script configurations.

#. Select **I agree to authorize MRS to scale out or scale in nodes based on the above rule**.

#. Click **OK**.
