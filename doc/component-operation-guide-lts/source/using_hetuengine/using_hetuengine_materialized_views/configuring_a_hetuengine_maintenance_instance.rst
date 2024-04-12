:original_name: mrs_01_24535.html

.. _mrs_01_24535:

Configuring a HetuEngine Maintenance Instance
=============================================

Scenario
--------

A maintenance instance is a special compute instance that performs automatic tasks. Maintenance instances are used to automatically refresh, create, and delete materialized views.

Only one compute instance can be set as a maintenance instance, and the maintenance instance can also carry original computing services at the same time.

Prerequisites
-------------

-  You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.
-  The compute instance to be configured must be in the stopped state.

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI.
#. Choose **Cluster** > **Services** > **HetuEngine** to go its service page.
#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Locate the row that contains the target instance, and click **Configure** in the **Operation** column.
#. Check whether **Maintenance Instance** in **Advanced Configuration** is set to **ON**. If not, change the value to **ON**.
#. After the modification is complete, select **Start Now** and click **OK**.
