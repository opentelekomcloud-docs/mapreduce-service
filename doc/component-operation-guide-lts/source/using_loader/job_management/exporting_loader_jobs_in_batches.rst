:original_name: mrs_01_1117.html

.. _mrs_01_1117:

Exporting Loader Jobs in Batches
================================

Scenario
--------

Loader allows existing jobs to be exported in batches.

Prerequisites
-------------

The current user has the **Edit** permission for the jobs to be exported or the **Jobs Edit** permission of the group to which the jobs belong.

Procedure
---------

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Click **Export**. The job export page is displayed.

#. Set **Batch Delete** to a job export type.

   -  **ALL**: exports all jobs.
   -  **Specify Job**: exports specified jobs. Select **Specify Job**. In the job list, select the jobs to be exported.
   -  **Specify Group**: exports all the jobs in a specified group. Select **Specify Group**. In the group list, select the group whose jobs are to be exported.

   **Export Password**: exports the connector password. If this parameter is selected, the password is exported as an encrypted string.

#. Click **OK** to start the job export. In the displayed dialog box, if the progress bar is 100%, the job import is complete.
