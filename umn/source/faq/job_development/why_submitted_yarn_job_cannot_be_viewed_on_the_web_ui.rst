:original_name: mrs_03_1223.html

.. _mrs_03_1223:

Why Submitted Yarn Job Cannot Be Viewed on the Web UI?
======================================================

After a Yarn job is created, it cannot be viewed if you log in to the web UI as the **admin** user.

-  The **admin** user is a user on the cluster management page. Check whether the user has the **supergroup** permission. Generally, only the user with the **supergroup** permission can view jobs.
-  Log in to Yarn as the user who submits jobs to view jobs on Yarn. Do not view the jobs using the **admin** user.
