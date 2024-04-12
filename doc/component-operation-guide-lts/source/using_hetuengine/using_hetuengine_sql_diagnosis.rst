:original_name: mrs_01_24838.html

.. _mrs_01_24838:

Using HetuEngine SQL Diagnosis
==============================

This section applies to MRS 3.2.0 or later.

Scenario
--------

The HetuEngine QAS module provides automatic detection, learning, and diagnosis of historical SQL execution records for more efficient online SQL O&M and faster online SQL analysis. After SQL diagnosis is enabled, the system provides the following capabilities:

-  Automatically detects and displays tenant-level and user-level SQL execution statistics in different time periods to cluster administrators, helping them quickly predict service running status and potential risks.
-  Automatically diagnoses large SQL statements, slow SQL statements, and related submission information, displays the information in multiple dimensions for cluster administrators, and provides diagnosis and optimization suggestions for these statements.

Prerequisites
-------------

-  The cluster is running properly and at least one QAS instance has been installed.
-  You have created a user for accessing the HetuEngine web UI, for example, **Hetu_user**. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Enabling SQL Diagnosis
----------------------

The SQL diagnosis function of HetuEngine is enabled by default. You can perform the following steps to configure other common parameters or retain the default settings:

#. Log in to FusionInsight Manager as user **Hetu_user**.
#. Choose **Cluster** > **Services** > **HetuEngine**. Click **Configurations** then **All Configurations**, click **QAS(Role)**, and select **SQL Diagnosis**. If **qas.sql.auto.diagnosis.enabled** is set to **true**, the SQL diagnosis function is enabled. In this case, you can configure recommended SQL diagnosis parameters based on service requirements.
#. Click **Save**.
#. Click **Instance**, select all QAS instances, click **More**, and select **Restart Instance**. In the displayed dialog box, enter the password to restart all QAS instances for the parameters to take effect.

Viewing SQL Diagnosis Results
-----------------------------

#. Log in to FusionInsight Manager as user **Hetu_user**.
#. Choose **Cluster** > **Services** > **HetuEngine** to go its service page.
#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Choose **SQL O&M** to view SQL diagnosis results.

   -  On the **Overview** page, you can view the overall running status of historical tasks, including the query duration distribution chart by segment, query user distribution chart, total submitted SQL queries, SQL execution success rate, average SQL query response time, number of queries, average execution time, and average waiting time.
   -  Choose **SQL Query Diagnostics** > **Slow Query Distribution** to view the slow query distribution of historical tasks, including:

      -  Slow SQL statistics: collects statistics on the number of slow queries (the query time is greater than the slow query threshold) submitted by each tenant.
      -  Top users with the maximum slow query requests: collects statistics on slow query statistics of each user. The statistics can be sorted in a list and exported.

   -  Choose **SQL Query Diagnostics** > **Slow Queries** to view the slow query list, diagnosis results, and optimization suggestions of historical tasks. Query results can be exported.

      .. note::

         The validity period of historical statistics depends on the JVM memory size of HSConsole instances and cannot exceed 60 days.
