:original_name: mrs_01_0415.html

.. _mrs_01_0415:

View Execution Records
======================

You can view the execution result of the bootstrap operation on the **Bootstrap Action** page.

Viewing the Execution Result
----------------------------

#. Log in to the MRS console.

#. In the left navigation pane, choose **Clusters** > **Active Clusters**. Click a cluster you want to query.

   The cluster details page is displayed.

#. On the cluster details page, click the **Bootstrap Action** tab. Information about the bootstrap actions added during cluster creation is displayed.

   .. note::

      -  You select **Before initial component start** or **After initial component start** in the upper right corner to query information about the related bootstrap actions.
      -  The last execution result is listed here. For a newly created cluster, the records of bootstrap actions executed during cluster creation are listed. If a cluster is expanded, the records of bootstrap actions executed on the newly added nodes are listed.

Viewing Execution Logs
----------------------

If you want to view the run logs of a bootstrap action, set **Action upon Failure** to **Continue** when adding the bootstrap action. And then, log in to each node to view the run logs in the **/var/log/Bootstrap** directory. If you add bootstrap actions before and after component start, you can distinguish bootstrap action logs of the two phases based on the timestamps.

You are advised to print logs in detail in the script so that you can view the detailed run result. MRS redirects the standard output and error output of the script to the log directory of the bootstrap action.
