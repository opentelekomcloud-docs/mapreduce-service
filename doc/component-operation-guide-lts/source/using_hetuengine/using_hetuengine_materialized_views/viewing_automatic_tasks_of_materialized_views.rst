:original_name: mrs_01_24505.html

.. _mrs_01_24505:

Viewing Automatic Tasks of Materialized Views
=============================================

Scenario
--------

View the status and execution result of an automatic HetuEngine task on HSConsol. You can periodically view the task execution status and evaluate the cluster health status.

Prerequisites
-------------

You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Choose **Automated Tasks**. On the displayed page, you can search for tasks by **Task Type**, **Status**, **Additional Info**, **Start Time**, or **End Time**. Fuzzy search is supported.

   +------------------+----------------------------------------------------------------------------------------------+
   | Search Criterion | Description                                                                                  |
   +==================+==============================================================================================+
   | Task Type        | **Refresh of materialized view**: refreshes materialized views.                              |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | **Recommendation of materialized view**: recommends materialized views.                      |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | **Auto create materialized view**: automatically creates materialized views.                 |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | **Drop auto created and stale materialized view**: automatically deletes materialized views. |
   +------------------+----------------------------------------------------------------------------------------------+
   | Status           | success                                                                                      |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | failed                                                                                       |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | waiting                                                                                      |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | running                                                                                      |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | skip_execute                                                                                 |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | time out                                                                                     |
   +------------------+----------------------------------------------------------------------------------------------+
   |                  | unknown                                                                                      |
   +------------------+----------------------------------------------------------------------------------------------+

#. Click **Search**. The tasks that match the search condition are displayed. You can click the **Link** on the **Task Details** column to show the specified task information.
