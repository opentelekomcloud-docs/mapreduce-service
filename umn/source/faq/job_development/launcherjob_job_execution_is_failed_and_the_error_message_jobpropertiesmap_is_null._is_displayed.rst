:original_name: mrs_03_1174.html

.. _mrs_03_1174:

LauncherJob Job Execution Is Failed And the Error Message "jobPropertiesMap is null." Is Displayed
==================================================================================================

The cause of the launcherJob failure is that the user who submits the job does not have the write permission on the **hdfs /mrs/job-properties** directory.

This problem is fixed in the 2.1.0.6 patch. You can also grant the write permission on the **/mrs/job-properties** directory to the synchronized user who submits the job on MRS Manager.
