:original_name: mrs_01_0416.html

.. _mrs_01_0416:

Adding a Bootstrap Action
=========================

Add a bootstrap action.

This operation applies to MRS 3.\ *x* or earlier clusters.

Procedure
---------

#. Log in to the MRS management console.
#. Choose **Clusters** > **Active Clusters** and click the name of your desired cluster.
#. On the page that is displayed, click the **Bootstrap Actions** tab.
#. Click **Add** and set parameters as prompted.

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

#. Click **OK** to save the configuration.
#. Click **Yes**.
