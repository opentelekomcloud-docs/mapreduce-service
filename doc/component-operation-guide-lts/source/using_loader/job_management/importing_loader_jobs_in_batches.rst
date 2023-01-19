:original_name: mrs_01_1116.html

.. _mrs_01_1116:

Importing Loader Jobs in Batches
================================

Scenario
--------

Loader allows all jobs of a configuration file to be imported in batches.

Prerequisites
-------------

The current user has the **Jobs Edit** permission of the group to which the jobs to be imported belong.

.. note::

   If the group to which the jobs to be imported belong does not exist, the group is automatically created first. The current user is the creator of the group and has the **Jobs Edit** permission of the group.

Procedure
---------

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Click **Import**. The Export Job page is displayed.
#. On the **Import** page, specify the path of the configuration file whose jobs are to be imported.
#. Click **Upload** to start the job import. In the displayed dialog box, if the progress bar is 100%, the job import is complete.
