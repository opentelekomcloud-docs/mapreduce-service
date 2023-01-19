:original_name: mrs_01_1114.html

.. _mrs_01_1114:

Migrating Loader Jobs in Batches
================================

Scenario
--------

Loader allows jobs to be migrated in batches from a group (source group) to another group (target group).

Prerequisites
-------------

-  The source group and target group exist.
-  The current user has the **Group Edit** permission for the source group and target group.
-  The current user has the **Jobs Edit** permission for the source group or the **Edit** permission for the jobs to be migrated.

Procedure
---------

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Click **Change Group**. The Job Migration page is displayed.
#. In **Source group**, select the group to which the jobs to be migrated belong; in **target group**, select the group to which the jobs are to be migrated.
#. Set **Select Change Type** to a migration type.

   -  **All**: migrates all the jobs in the source group to the target group.
   -  **Specify Job**: migrates the specified jobs in the source group to the target group. Select **Specify Job**. In the job list, select the jobs to be migrated.

#. Click **OK** to start job migration. In the displayed dialog box, if the progress bar is 100%, the job migration is complete.
