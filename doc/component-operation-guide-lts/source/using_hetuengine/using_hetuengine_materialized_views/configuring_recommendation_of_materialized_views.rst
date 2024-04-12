:original_name: mrs_01_24776.html

.. _mrs_01_24776:

Configuring Recommendation of Materialized Views
================================================

Scenario
--------

HetuEngine QAS module provides automatic detection, learning, and diagnosis of historical SQL execution records. After the materialized view recommendation function is enabled, the system can automatically learn and recommend the most valuable materialized view SQL statements, enabling HetuEngine to have the automatic precomputation acceleration capability. In related scenarios, the online query efficiency is improved by multiple times, and the system load pressure is effectively reduced.

Prerequisites
-------------

-  The cluster is running properly and at least one QAS instance has been installed.
-  You have created a user for accessing the HetuEngine web UI, for example, **Hetu_user**. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

.. _mrs_01_24776__en-us_topic_0000001521080921_section109434212018:

Enabling Materialized View Recommendation
-----------------------------------------

#. Log in to FusionInsight Manager as user **Hetu_user**.

#. Choose **Cluster** > **Services** > **HetuEngine** and then choose **Configurations** > **All Configurations**. In the navigation tree, choose **QAS(Role)** > **Materialized View Recommendation**. Set materialized view recommendation parameters by referring to :ref:`Table 1 <mrs_01_24776__en-us_topic_0000001521080921_table49551729155011>` and retain the default values for other parameters.

   .. _mrs_01_24776__en-us_topic_0000001521080921_table49551729155011:

   .. table:: **Table 1** Materialized view recommendation parameters

      +--------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                      | Example Value | Description                                                                                                                                                            |
      +================================+===============+========================================================================================================================================================================+
      | qas.enable.auto.recommendation | true          | Whether to enable materialized view recommendation. The default value is **false**.                                                                                    |
      +--------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | qas.sql.submitter              | default,zuhu1 | Name of the tenant for which the materialized view recommendation function is enabled. Use commas (,) to separate multiple tenants.                                    |
      +--------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | qas.schedule.fixed.delay       | 1d            | Interval for recommending materialized views. Once a day is recommended.                                                                                               |
      +--------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | qas.threshold.for.mv.recommend | 0.05          | Filtering threshold of materialized view recommendation. The value ranges from **0.001** to **1**. You are advised to adjust the value based on the site requirements. |
      +--------------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Save**.

#. Click **Instance**, select all QAS instances, click **More**, and select **Restart Instance**. In the displayed dialog box, enter the password to restart all QAS instances for the parameters to take effect.

.. _mrs_01_24776__en-us_topic_0000001521080921_section051233712276:

Viewing Materialized View Recommendation Results
------------------------------------------------

#. Log in to FusionInsight Manager as user **Hetu_user**.

#. Choose **Cluster** > **Services** > **HetuEngine** to go its service page.

#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

#. Choose **SQL O&M** > **Automatic MV Recommendation**. You can search for materialized views by tenant, status, recommendation period, and materialized view name. Fuzzy search is supported. You can export the recommendation result of a specified materialized view.

   The status of a materialized view task can be:

   .. table:: **Table 2** Status of a materialized view task

      ============= =============== =========== =======================
      Status Name   Description     Status Name Description
      ============= =============== =========== =======================
      To Be Created To be created   Deleting    Terminating
      Creating      Creating        Deleted     Terminated
      Created       Created         Planning    Being planned
      Failed        Creation failed Aborted     Aborted
      Updating      Updating        Duplicated  Repeated recommendation
      ============= =============== =========== =======================
