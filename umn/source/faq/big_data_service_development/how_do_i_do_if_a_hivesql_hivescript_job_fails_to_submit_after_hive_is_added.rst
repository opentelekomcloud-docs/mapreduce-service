:original_name: mrs_03_1200.html

.. _mrs_03_1200:

How Do I Do If a "hivesql/hivescript" Job Fails to Submit After Hive Is Added?
==============================================================================

This issue occurs because the **MRS CommonOperations** permission bound to the user group to which the user who submits the job belongs does not include the Hive permission after being synchronized to Manager. To solve this issue, perform the following operations:

#. Add the Hive service.
#. Log in to the IAM console and create a user group. The policy bound to the user group is the same as that of the user group to which the user who submits the job belongs.
#. Add the user who submits the job to the new user group.
#. Refresh the cluster details page on the MRS console. The status of IAM user synchronization is **Not synchronized**.
#. Click **Synchronize** on the right of **IAM User Sync**. Go back to the previous page. In the navigation pane on the left, choose **Operation Logs** and check whether the user is changed.

   -  If yes, submit the Hive job again.
   -  If no, check whether all the preceding operations are complete.

      -  If yes, contact the O&M personnel.
      -  If no, submit the Hive job after the preceding operations are complete.
