:original_name: mrs_01_1118.html

.. _mrs_01_1118:

Viewing Historical Job Information
==================================

Scenario
--------

Query the execution status and execution duration of a Loader job during routine maintenance. You can perform the following operations on the job:

-  Dirty Data: Query data that fails to be processed or data that is filtered out during job execution, and check which source data does not meet transformation or cleaning rules.
-  Logs: Query log information about job execution in MapReduce.

Prerequisites
-------------

You have obtained the username and password for logging in to the Loader WebUI.

Procedure
---------

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Query historical records of a Loader job.

   a. Locate the row that contains the job to be viewed.

   b. As shown in the following figure, click **History** to view the job execution history.


      .. figure:: /_static/images/en-us_image_0000001349259089.png
         :alt: **Figure 2** Viewing historical records

         **Figure 2** Viewing historical records

      .. table:: **Table 1** Parameters

         +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
         | Name                              | Description                                                                                                                                       |
         +===================================+===================================================================================================================================================+
         | Rows/Files Read                   | Indicates the number of rows (files) read from the input source.                                                                                  |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
         | Rows/Files Written                | Number of rows (files) written to the output source.                                                                                              |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
         | Rows/Files Overridden             | -  Indicates the number of bad rows (files) recorded during transformation. The input format is incorrect, so transformation cannot be performed. |
         |                                   | -  Number of rows that are skipped after filtering conditions are configured during conversion.                                                   |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
